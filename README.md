# GPT2-Sentiment-Control or Controllable Text Generation with Fine-Tuned GPT-2

## Overview
This project explores controllable language generation by fine-tuning a pre-trained GPT-2 model. The objective was to steer the model's text generation based on two specific constraints: **exact target lengths** and **sentiment polarity** (positive/negative). 

## Objectives
1. **Length Control:** Fine-tune GPT-2 to generate text matching a precise word count using the Open WebText dataset.
2. **Sentiment Control:** Modify the model to reliably generate positive or negative restaurant reviews using the Yelp Polarity dataset.

## Methodology & Architecture
* **Base Model:** Hugging Face `GPT-2`
* **Tokenizer Customization:** Resized the model's embedding layer to incorporate custom control tokens (`<len>`, `<sentiment>`, `<text>`).
* **Training Setup:** * Length Control: Evaluated text generation for target lengths ranging from 5 to 30 words.
  * Sentiment Control: Fine-tuned on 10,000 balanced samples from the Yelp Polarity dataset.

## Key Results

### 1. Sentiment Control Accuracy
To evaluate the success of the sentiment generation, **DistilBERT** has been utilized as an automated classifier to verify if the generated text matched the prompted sentiment token.
* **Positive Prompt Accuracy:** 90%
* **Negative Prompt Accuracy:** 85%
* **Overall Accuracy:** 87.5%

*Example Generation (Positive Prompt):*
> "<sentiment> positive <text> Excellent service. We had the same pizza as the other reviewers but opted to go with the larger selection of toppings. The pizza was fresh and very tasty..."

### 2. Length Control Performance
The model demonstrated strong adherence to length constraints, with deviations remaining minimal across various targets.
* **Average Length Control Error:** ~1.50 words.
* Reached near-perfect accuracy for mid-length targets (e.g., exactly 10 or 20 words).

## Key Takeaways & Limitations
* **Stable Optimization:** Gradient norms remained stable (between 4-5) without exploding or vanishing gradients, proving the viability of the training parameters.
* **Domain Adaptation:** The model successfully adopted domain-specific vocabulary (e.g., restaurant terminology) from the Yelp dataset, generating coherent and contextually appropriate reviews.
* **Future Improvements:** Implementing additional penalty functions during training could further reduce length deviation errors for longer text generation (>30 words). 
