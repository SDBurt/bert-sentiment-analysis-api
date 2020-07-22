# Fine-tuned BERT model for Sentiment Classification

## Summary

This project holds the code for a fine-tuned BERT NLP model which classifies text as either negative, neutral, or positive sentiment. The code and idea for this model was based on the tutorials by Venelin. This project specifically was based on [Deploy bert for sentiment analysis as rest api](https://www.curiousily.com/posts/deploy-bert-for-sentiment-analysis-as-rest-api-using-pytorch-transformers-by-hugging-face-and-fastapi/).

This API uses `PyTorch`, `Transformers by HuggingFace`, and `FastAPI`

## Setup

1. Install `pipenv` if it is not already installed on your machine.
2. Run `pipenv install`.
3. Run `uvicorn sentiment_analyzer.api:app`
4. Install `httpie` and use tutorials example http request (terminal): `http POST http://localhost:8000/predict text="This app is a total waste of time!"`

## Output & Observations

Output of `http POST http://localhost:8000/predict text="This app is a total waste of time!"`:

```json
HTTP/1.1 200 OK
content-length: 169
content-type: application/json
date: Wed, 22 Jul 2020 17:33:44 GMT
server: uvicorn

{
    "confidence": 0.9998829364776611,
    "probabilities": {
        "negative": 0.9998829364776611,
        "neutral": 7.627315790159628e-05,
        "positive": 4.076507320860401e-05
    },
    "sentiment": "negative"
}
```

The output appears pretty accurate but it's not perfect yet.

Output of `http POST http://localhost:8000/predict text="This game has its pros and cons. It's fun at first but gets boring after a few days."`

```json
HTTP/1.1 200 OK
content-length: 169
content-type: application/json
date: Wed, 22 Jul 2020 18:00:31 GMT
server: uvicorn

{
    "confidence": 0.999651312828064,
    "probabilities": {
        "negative": 0.00010982507228618488,
        "neutral": 0.00023884115216787905,
        "positive": 0.999651312828064
    },
    "sentiment": "positive"
}
```

It appears that the words like **fun** overpowers the words like **boring**, even when the context of the comment is negative.

## References
- [Model Training Tutorial](https://www.curiousily.com/posts/sentiment-analysis-with-bert-and-hugging-face-using-pytorch-and-python/)
- [Model API Tutorial](https://www.curiousily.com/posts/deploy-bert-for-sentiment-analysis-as-rest-api-using-pytorch-transformers-by-hugging-face-and-fastapi/)
- [HuggingFace Github](https://github.com/huggingface)
- [FastAPI](https://fastapi.tiangolo.com/)
- [PyTorch](https://pytorch.org/)