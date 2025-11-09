# NIRVAAH AI Model Documentation (Text)

**Model File:** `symptom_model.tflite`
**Created:** 09/11/2025

---

## 1. Description
This model takes an English text phrase describing medical symptoms and classifies it into one of five categories.

---

## 2. Input Details
The model expects **two** inputs in a specific order:

1.  `input_ids`: An integer tensor of shape `[1, 128]`. This is the tokenized version of the input sentence.
2.  `attention_mask`: An integer tensor of shape `[1, 128]`. This tells the model which tokens are real and which are padding.

**Frontend Preprocessing Steps:**
The frontend React Native app must use a JavaScript version of the `'distilbert-base-uncased'` tokenizer to convert the user's string into these two tensors. The input string must be padded or truncated to exactly 128 tokens.

---

## 3. Output Details
The model has **one** output:

1.  `output_0` (or `logits`): A float tensor of shape `[1, 5]`. This is an array of raw scores for each of the 5 possible classes.

**Frontend Postprocessing Steps:**
1.  Find the index of the highest value in the output array. (e.g., using `argmax`).
2.  Use the `label_map` below to convert this index (0, 1, 2, 3, or 4) back to a human-readable diagnosis string.

---

## 4. Label Map (CRITICAL)
This maps the model's output index to the diagnosis string.

```json 
{0: 'Acne', 1: 'Infected wound', 2: 'Joint pain', 3: 'Knee pain', 4: 'Shoulder pain'}