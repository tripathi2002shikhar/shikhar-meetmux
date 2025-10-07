README.txt
AI–ML Developer Intern - Chat-Reply Recommendation System

1. OVERVIEW
--------------------------------------------------------------------------------
This repository contains the solution for the offline Chat-Reply Recommendation System. The system predicts User A's response following a message from User B, using conversation history as context.

Model: Fine-tuned DistilGPT-2 (Causal Language Modeling)
Training: Custom, optimized PyTorch training loop (to ensure compatibility with limited offline libraries, avoiding 'accelerate' and 'datasets').
Context Handling: Uses special tokens (<USER_A>, <USER_B>, <REPLY>) to structure conversation history.

2. SUBMISSION FILES
--------------------------------------------------------------------------------
- ChatRec_Model.ipynb: The main code file containing all preprocessing, the custom PyTorch training loop, and evaluation functions.
- Model.joblib: The final, trained PyTorch model object (required submission format).
- Report.pdf: Technical justification, model choice, optimization, and evaluation metrics summary.
- ReadMe.txt: This file.

3. EXECUTION INSTRUCTIONS (Running the Code)
--------------------------------------------------------------------------------
The system is designed to run entirely offline using the preloaded libraries.

Dependencies:
- Python 3.10+
- Preloaded Libraries: pandas, numpy, torch, transformers, scikit-learn, nltk, joblib, rouge_score, tqdm.

Steps to Run:

1. Setup: Ensure the conversation data file ('conversationfile.xlsx - userAuserB.csv') is accessible.
2. Load Notebook: Open ChatRec_Model.ipynb.
3. Data and Setup: Run sections 1, 2, and 3 (Data Loading, Formatting, Tokenization, and Model/Optimizer setup).
4. Training: Execute the training loop (Section 4). This fine-tunes the DistilGPT-2 model. This is the primary time-consuming step (approx. 30-60 minutes depending on hardware).
5. Saving Model: AFTER the training loop is complete, execute the saving step:
   joblib.dump(model, "Model.joblib")
6. Evaluation: Run Section 5 (Reply Generation and Evaluation). This will calculate BLEU, ROUGE-L, and Perplexity metrics using the best-performing model.

4. INFERENCE/PREDICTION EXAMPLE
--------------------------------------------------------------------------------
The 'generate_reply' function is used for inference. It requires the model, tokenizer, the last message from User B, and the list of preceding context turns.

Example Usage (Run this block after training is complete in the notebook):

from_user_b = "Did you manage to fix the bug in the timeline function?"
history = [
    "<USER_A> I'm looking into it now.",
    "<USER_B> Okay, let me know if you need logs."
]

predicted_reply = generate_reply(model, tokenizer, from_user_b, history)
print("Predicted Reply from User A:", predicted_reply)