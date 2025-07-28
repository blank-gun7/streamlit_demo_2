# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

### Running the Application
```bash
streamlit run app.py
```

### Setup and Installation
```bash
# Install dependencies
pip install -r requirements.txt

# Set up environment variables (for local development)
cp .env.example .env
# Edit .env and add your OpenAI API key
```

### Testing and Validation
- Always test the application locally before committing changes
- Verify all user flows: login, data upload, analysis generation, and chatbot interactions
- Test both investee and investor user journeys

## High-Level Architecture

This is a multi-user Streamlit application for revenue analytics with AI-powered insights. The architecture consists of several key layers:

### User Management System
- **Role-Based Access Control**: Two user types (investee, investor) with different capabilities
- **Authentication**: SQLite-based user management with password hashing
- **Company Relationships**: Many-to-many relationships between investors and companies

### Data Processing Pipeline
- **Multi-Format Support**: Handles both JSON files and Excel uploads (.xlsx, .xls)
- **Automatic Type Detection**: Intelligently categorizes data based on content and filenames
- **Data Normalization**: Converts various data types to JSON-serializable formats
- **Five Core Analysis Types**:
  - Quarterly Revenue & QoQ Growth
  - Revenue Bridge & Churn Analysis
  - Country-wise Revenue Analysis
  - Customer Concentration Analysis
  - Month-on-Month Revenue Trends

### AI Integration Architecture
- **OpenAI GPT-4 Integration**: Powers executive summaries and interactive chatbots
- **Context-Aware Analysis**: Each analysis type has tailored prompts for relevant insights
- **Fallback Mechanisms**: Graceful degradation when AI services are unavailable
- **Session-Based Chat**: Maintains conversation history per analysis view

### Database Schema
```sql
-- Core tables
users (id, username, password_hash, user_type, company_name)
companies (id, company_name, investee_id)
investor_companies (investor_id, company_id) -- Many-to-many relationship
company_data (company_id, data_type, data_content) -- JSON storage
```

## Key Technical Components

### Data Upload System
- **Excel Processing**: Multi-sheet support with automatic header detection
- **Data Type Conversion**: Handles datetime, numeric, and text data with proper serialization
- **Error Handling**: Comprehensive error reporting for data upload issues
- **Type Classification**: Automatic categorization based on sheet names and content

### Visualization Engine
- **Plotly Integration**: Interactive charts for all analysis types
- **Responsive Design**: Charts adapt to container width
- **Custom Styling**: Professional color schemes and layouts
- **Data Filtering**: Dynamic filtering capabilities for large datasets

### AI-Powered Features
- **Executive Summaries**: Automatically generated insights for each analysis type
- **Interactive Chatbots**: Context-aware Q&A for each data view
- **Professional Analysis**: Business intelligence focused prompts and responses
- **Error Recovery**: Fallback summaries when AI is unavailable

### Report Generation
- **PDF Export**: Uses reportlab for professional report generation
- **JSON Export**: Structured data export with metadata
- **Processing Animation**: 30-second analysis simulation for user experience
- **Download Management**: Proper file naming and MIME type handling

## Data Structures

### JSON Data Formats
Each analysis type expects specific JSON structures:

**Quarterly Revenue**:
```json
[
  {
    "Customer Name": "string",
    "Quarter 3 Revenue": number,
    "Quarter 4 Revenue": number,
    "Variance": number,
    "Percentage of Variance": number
  }
]
```

**Revenue Bridge**:
- Contains churned, new, expansion, and contraction revenue fields
- Used for waterfall chart generation

**Geographic Analysis**:
- Country-wise revenue distribution
- Supports yearly revenue analysis

**Customer Concentration**:
- Customer portfolio analysis
- Revenue concentration risk assessment

**Monthly Trends**:
- Month-over-month revenue patterns
- Variance analysis and seasonality detection

## Development Guidelines

### Code Organization
- **Single File Architecture**: Main application logic in `app.py`
- **Class-Based Structure**: 
  - `DatabaseManager`: Handles all SQLite operations
  - `AuthManager`: Manages user authentication
  - `DashboardVisualizer`: Creates charts and visualizations
  - `OpenAIChatbot`: Handles AI interactions
- **Functional Components**: Display functions for each analysis type

### Error Handling Patterns
- Comprehensive try-catch blocks for data processing
- Graceful fallbacks for AI service failures
- User-friendly error messages with debugging information
- Safe JSON serialization with custom handlers

### AI Integration Best Practices
- Context-specific prompts for each analysis type
- Token limit management (8000 chars for data context)
- Temperature settings optimized for business analysis (0.2-0.3)
- Fallback content generation when API is unavailable

### Database Operations
- Connection management with proper closing
- SQL injection prevention through parameterized queries
- Atomic operations for data consistency
- Foreign key relationships properly maintained

## Security Considerations

- Password hashing using SHA-256
- Environment variable management for API keys
- SQL injection prevention
- Session state management for user data isolation
- No sensitive information in logs or error messages

## Important Rules from Existing Configuration

1. **Professional Standards**: All changes should maintain professional code quality
2. **Research-Driven Development**: Always research multiple approaches before implementation
3. **Thorough Testing**: Test all changes locally before committing
4. **Logic Preservation**: Ensure existing functionality remains intact when making changes
5. **Version Control**: Commit all changes without AI attribution to maintain professional appearance

## Common Workflows

### Adding New Analysis Types
1. Create display function following existing patterns
2. Add data type detection in upload logic
3. Create AI prompt template for the new analysis
4. Add tab to the main interface
5. Update database schema if needed

### Debugging Data Upload Issues
1. Check Excel file format and structure
2. Verify header detection logic
3. Review data type conversion functions
4. Test JSON serialization process
5. Validate database storage

### Extending AI Capabilities
1. Review existing prompt templates
2. Test new prompts with sample data
3. Implement fallback mechanisms
4. Add appropriate error handling
5. Update chat interface as needed

### Performance Optimization
- Monitor Streamlit session state usage
- Optimize database queries with proper indexing
- Implement data pagination for large datasets
- Cache expensive operations where appropriate
- Consider async operations for AI API calls

## Deployment Notes

### Local Development
- Requires Python 3.9+ with all dependencies from requirements.txt
- OpenAI API key required for full functionality
- SQLite database automatically created on first run

### Production Deployment
- Streamlit Cloud deployment supported
- Configure secrets for OpenAI API key
- Database persists across deployments
- Static assets (logo, JSON files) included in deployment

This architecture supports a complete revenue analytics workflow from data upload through AI-powered analysis and reporting, designed for professional investment analysis use cases.