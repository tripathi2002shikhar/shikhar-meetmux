README.txt
AI–ML Developer Intern - Chat-Reply Recommendation System

1. OVERVIEW
--------------------------------------------------------------------------------
This repository contains the solution for the offline Chat-Reply Recommendation System. The system predicts User A's response following a message from User B, using conversation history as context.

Model: Fine-tuned DistilGPT-2 (Causal Language Modeling)
Training: Custom, optimized PyTorch training loop (using only core preloaded libraries).

2. SUBMISSION FILES
--------------------------------------------------------------------------------
- ChatRec_Model.ipynb: The main code file containing all logic.
- Model.joblib: The final, trained PyTorch model object (required submission format).
- Report.pdf: Technical justification, model choice, optimization, and evaluation metrics summary.
- ReadMe.txt: This file.

3. MODEL ACCESS LINKS (Google Drive)
--------------------------------------------------------------------------------
The final model and best checkpoint state dictionary are available via the following public links:

- Complete Model : https://drive.google.com/file/d/1vn9mwAct6QY7D0T4XrkptGRpn3cpZeWT/view?usp=sharing
- Complete Project : https://drive.google.com/drive/folders/1TSP8pmQv9jhrRZtBN0i-cNfchh-yMyC_?usp=sharing

4. EXECUTION INSTRUCTIONS (Running the Code)
--------------------------------------------------------------------------------
Dependencies:
- Python 3.10+
- Preloaded Libraries: pandas, numpy, torch, transformers, scikit-learn, nltk, joblib, rouge_score, tqdm.

Steps to Run:

1. Setup: Ensure the conversation data file ('conversationfile.xlsx - userAuserB.csv') is accessible.
2. Load Notebook: Open ChatRec_Model.ipynb.
3. Training: Execute the training loop (starting in Section 4). This fine-tunes the DistilGPT-2 model.
4. Saving Model: AFTER the training loop is complete (and the best model is saved locally as 'best_model.pt'), execute the final submission step:
   joblib.dump(model, "Model.joblib")
5. Evaluation: Run the 'evaluate_generation' function to calculate and report the final metrics (BLEU, ROUGE, PPL).

5. INFERENCE/PREDICTION EXAMPLE
--------------------------------------------------------------------------------
Example Usage (Run this block after training is complete in the notebook):

from_user_b = "Did you manage to fix the bug in the timeline function?"
history = [
    "<USER_A> I'm looking into it now.",
    "<USER_B> Okay, let me know if you need logs."
]

predicted_reply = generate_reply(model, tokenizer, from_user_b, history)
print("Predicted Reply from User A:", predicted_reply)
