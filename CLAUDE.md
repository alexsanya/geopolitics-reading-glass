# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a YouTube comments analysis project that scrapes, filters, and performs multi-dimensional AI-powered classification of YouTube comments using DSPy (Declarative Self-improving Language Programs). The project analyzes comments from a CaspianReport video about Israel's strike on Qatar.

## Key Dependencies & Framework

- **DSPy**: Core framework for building language model programs with structured signatures
- **Python 3.12+**: Required Python version
- **UV**: Package manager (uv.lock present)
- **Pandas**: Data manipulation and analysis
- **OpenAI API**: Language model backend (GPT-5 via custom endpoint)
- **ScrapeCreators API**: YouTube comments scraping service
- **Jupyter**: Interactive development environment

## Environment Setup

### Required Environment Variables
Create a `.env` file with:
```
OPENAI_API_KEY=your_openai_api_key
OPENAI_BASE_URL=your_openai_base_url  # Custom endpoint
SCRAPPER_API_KEY=your_scrapecreators_api_key  # For YouTube scraping
```

### Installation Commands
```bash
# Install dependencies
uv install

# Start Jupyter (for interactive development)
uv run jupyter lab
```

## Project Architecture

### Data Pipeline Flow
1. **Data Collection** (`DataCollection.ipynb`):
   - YouTube comments scraping via ScrapeCreators API
   - Video transcript extraction (using Claude Desktop with youtube_transcript MCP)
   - Raw data storage in JSON format

2. **Comments Classification** (`CommentsClassification.ipynb`):
   - AI-powered relevance filtering to remove off-topic comments
   - Multi-dimensional comment analysis using DSPy signatures
   - Sentiment analysis toward key actors (Israel, US, Qatar, Hamas)
   - Intelligence and insightfulness scoring

3. **Additional Analysis** (`FedDecision.ipynb`):
   - Appears to contain FOMC/Federal Reserve news classification (different use case)

### DSPy Signature Architecture

The project uses DSPy's signature-based approach for structured AI analysis:

- **RelevanceAssesor**: Filters comments by topical relevance (1-5 scale)
- **ClassifyComment**: Multi-dimensional analysis including:
  - Topic tagging from predefined VideoTopic enum
  - Attitude scoring toward Israel, US, Qatar, Hamas (1-10 scale)
  - Intelligence assessment (1-5 scale)
  - Insightfulness scoring (1-5 scale)
  - Emotional intensity measurement (1-5 scale)

### Data Storage Structure

- `data/output.json`: Raw scraped comments from YouTube API
- `data/youtube_comments.csv`: Processed comments DataFrame
- `data/video_transcript.md`: Video transcript in Markdown format
- `data/df_low_engagement.csv`: Comments with <6 likes (for relevance checking)
- `data/all_relevant_comments.csv`: Filtered relevant comments
- `data/comments_classified.csv`: Final classified dataset with all dimensions
- `data/comments_classified.pkl`: Pickle format for complex data structures
- `data/reasoning_all_results.pkl`: AI reasoning explanations for classifications

## Development Workflow

### Running the Analysis Pipeline
1. Start with `DataCollection.ipynb` to scrape comments
2. Process through `CommentsClassification.ipynb` for AI analysis
3. Results are automatically saved to CSV/pickle formats

### DSPy Configuration
The project configures DSPy with:
```python
lm = dspy.LM("openai/gpt-5", api_key=os.environ["OPENAI_API_KEY"],
             api_base=os.environ["OPENAI_BASE_URL"],
             temperature=1.0, max_tokens=16000)
dspy.configure(lm=lm)
```

### Async Processing
Large-scale comment processing uses async/await patterns with:
- Concurrent API calls (max 10 simultaneous)
- Progress tracking with tqdm
- Chunked processing (100 comments per chunk)
- Rate limiting between chunks

## Key Design Patterns

### Signature-Based AI Development
Uses DSPy signatures for structured LLM interactions rather than raw prompts:
- Type-safe input/output definitions
- Automatic prompt optimization
- Chain-of-thought reasoning integration

### Multi-Dimensional Analysis
Comments are analyzed across multiple dimensions simultaneously:
- Topic identification using predefined enums
- Attitude measurement with confidence scoring
- Qualitative assessment (intelligence, insight, emotion)

### Relevance Filtering Pipeline
Two-stage filtering approach:
1. High-engagement comments (6+ likes) automatically included
2. Low-engagement comments filtered through AI relevance assessment
3. Only relevant comments proceed to full analysis

## Testing & Quality Assurance

No formal test suite present. Quality assurance relies on:
- Sample analysis and manual validation of AI classifications
- Confidence scoring for AI assessments
- Data backup at each processing stage

## Important Notes

- The project processes real YouTube comments about sensitive political topics
- AI classification results should be interpreted carefully given the subjective nature of sentiment analysis
- Large API costs can be incurred due to extensive LLM usage for classification
- All classification includes reasoning/explanation for transparency