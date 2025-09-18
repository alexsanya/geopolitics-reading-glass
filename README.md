# YouTube Comments Analysis: Israel's Strike on Qatar

![Project Cover](cover.png)

*AI-powered analysis of YouTube comments using DSPy for multi-dimensional sentiment classification*

## Overview

This project performs comprehensive analysis of YouTube comments from a CaspianReport video about "How Israel's Strike on Qatar Shatters the Middle East." Using advanced AI techniques with DSPy (Declarative Self-improving Language Programs), it classifies comments across multiple dimensions including sentiment toward key geopolitical actors, intelligence assessment, and emotional intensity.

## Key Features

- **<¯ Smart Relevance Filtering**: AI-powered filtering to identify topically relevant comments
- **=Ê Multi-Dimensional Analysis**: Sentiment analysis toward Israel, US, Qatar, and Hamas
- **>à Intelligence Scoring**: Assessment of comment sophistication and reasoning quality
- **=¡ Insight Classification**: Categorization of comment types (factual corrections, historical parallels, etc.)
- **=
 Emotional Analysis**: Measurement of emotional intensity and inflammatory content
- **¡ Async Processing**: Efficient parallel processing of large comment datasets

## Architecture

### Data Pipeline

1. **Data Collection** (`DataCollection.ipynb`)
   - YouTube comments scraping via ScrapeCreators API
   - Video transcript extraction using youtube_transcript MCP
   - Raw data storage and preprocessing

2. **AI Classification** (`CommentsClassification.ipynb`)
   - Relevance filtering (comments with <6 likes assessed by AI)
   - Multi-dimensional sentiment analysis using DSPy signatures
   - Confidence scoring and reasoning extraction

3. **Results & Analysis**
   - Structured data export (CSV/Pickle formats)
   - Comprehensive classification with AI reasoning
   - Quality metrics and validation

### DSPy Signatures

The project uses two main DSPy signatures for structured AI analysis:

- **`RelevanceAssesor`**: Filters comments by topical relevance (1-5 scale)
- **`ClassifyComment`**: Performs comprehensive multi-dimensional analysis:
  - Topic identification from predefined enums
  - Attitude scoring (1-10 scale) toward key actors
  - Intelligence assessment (1-5 scale)
  - Insightfulness and emotional intensity scoring

## Installation & Setup

### Prerequisites

- Python 3.12+
- OpenAI API access (GPT-5)
- ScrapeCreators API key for YouTube scraping

### Environment Setup

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd comments-disection
   ```

2. **Install dependencies**
   ```bash
   uv install
   ```

3. **Configure environment variables**
   Create a `.env` file:
   ```env
   OPENAI_API_KEY=your_openai_api_key
   OPENAI_BASE_URL=your_openai_base_url
   SCRAPPER_API_KEY=your_scrapecreators_api_key
   ```

4. **Start Jupyter Lab**
   ```bash
   uv run jupyter lab
   ```

## Usage

### Running the Analysis Pipeline

1. **Data Collection**: Execute `DataCollection.ipynb` to scrape YouTube comments and extract video transcript

2. **Classification**: Run `CommentsClassification.ipynb` to perform AI-powered analysis:
   - Filters ~878 low-engagement comments for relevance
   - Classifies ~649 relevant comments across multiple dimensions
   - Generates reasoning explanations for all classifications

3. **Results**: Access processed data in multiple formats:
   - `data/comments_classified.csv`: Human-readable classification results
   - `data/comments_classified.pkl`: Complete data with complex structures
   - `data/reasoning_all_results.pkl`: AI reasoning explanations

### Key Insights from Analysis

- **16.21%** of comments classified as irrelevant to video topic
- **649** relevant comments analyzed across multiple dimensions
- Attitude distributions toward key actors with confidence scoring
- Intelligence and insightfulness metrics for content quality assessment

## Technical Implementation

### DSPy Configuration

```python
lm = dspy.LM("openai/gpt-5",
             api_key=os.environ["OPENAI_API_KEY"],
             api_base=os.environ["OPENAI_BASE_URL"],
             temperature=1.0, max_tokens=16000)
dspy.configure(lm=lm)
```

### Async Processing Pattern

- **Concurrent Processing**: Up to 10 simultaneous API calls
- **Chunked Analysis**: 100 comments per processing batch
- **Progress Tracking**: Real-time progress with tqdm
- **Rate Limiting**: Automatic delays between chunks

### Data Quality Measures

- **Confidence Scoring**: All classifications include confidence metrics
- **Reasoning Extraction**: AI explanations for transparency
- **Validation Sampling**: Manual review of classification samples
- **Incremental Backups**: Data saved at each processing stage

## Data Schema

### Comment Classification Fields

- `mentioned_topics`: Relevant video topics from predefined enum
- `attitude_towards_*`: Sentiment scoring (1-10) toward key actors
- `attitude_confidence`: Confidence in sentiment assessments
- `intelligence_score`: Sophistication assessment (1-5)
- `insightfulness_score`: Value-added measurement (1-5)
- `emotional_score`: Emotional intensity (1-5)
- `insight_type`: Category of contribution (factual correction, historical parallel, etc.)

## Dependencies

- **DSPy**: Structured language model programming
- **Pandas**: Data manipulation and analysis
- **Matplotlib/Seaborn**: Data visualization
- **asyncio/tqdm**: Async processing with progress tracking
- **dotenv**: Environment variable management

## Notes & Considerations

- **API Costs**: Extensive LLM usage for classification can incur significant costs
- **Subjective Analysis**: Sentiment classification results should be interpreted carefully
- **Political Sensitivity**: Project analyzes comments on sensitive geopolitical topics
- **Data Privacy**: All data is from public YouTube comments

## Contributing

This project demonstrates advanced AI application patterns for social media analysis. Contributions welcome for:
- Additional classification dimensions
- Improved DSPy signature designs
- Visualization and reporting enhancements
- Performance optimizations

## License

[Add your license information here]

---

*This project showcases the power of DSPy for structured AI analysis, demonstrating how modern language models can be used for sophisticated social media sentiment analysis and content classification.*