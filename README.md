# Conversational-chatbot-with-finutuned-BART

**Fine‑Tuned Conversational Chatbot using DioloGPT with BART for Summarization**

A two‑stage, summary‑driven conversational chatbot that uses a LoRA‑adapted BART summarizer and DialoGPT generator.  Summaries of the dialogue history are generated on‑the‑fly and used as context to produce coherent, context‑aware responses.

---

## Repository Structure

```plaintext
├──── Task1_Dataset_preperation.ipynb     # Generate ground‑truth summaries using Llama 3 on DailyDialog
│──── Task2_Finetune_BARTXsum.ipynb        # Fine‑tune BART‑Large‑XSum with LoRA adapters
│──── Loss_evaluation_and_chatbot.ipynb # Evaluate losses & launch interactive chatbot demo
│
├── data/                             # Processed dataset and Llama 3–generated summaries
│   ├── Llama_summaries.csv            # Golden summaries from Llama 3 (2,000 conversations) with Raw and preprocessed dialogues
│   ├── bartXsum_summaries.csv                    
│   ├── bartXsumFinetuned_summaries.csv
│   └── bartXsum_val_summaries.csv
│
├── model/                            # Final checkpoint and adapter files
│   ├── checkpoint-2430/              # LoRA‑adapted BART weights and config
│   ├── adapter_config.json
│   ├── adapter_model.safetensors
│   ├── merges.txt
│   ├── special_tokens_map.json
│   ├── tokenizer_config.json
│   ├── vocab.json
│   └── training_args.bin             # Training arguments (optional)
│
├── requirements.txt                  # Python dependencies and versions
└── README.md                         # This file
```

---

## 🚀 Quick Start

1. **Clone the repository**

   ```bash
   git clone https://github.com/Tanmay-jam/Conversational-chatbot-with-finetuned-BART.git
   cd Conversational-chatbot-with-finetuned-BART
   ```

2. **Set up a Python environment**

   ```bash
   python3 -m venv venv
   source venv/bin/activate        # Linux/macOS
   venv\Scripts\activate         # Windows
   pip install -r requirements.txt
   ```

3. **Run the notebooks**

   - **01\_data\_preparation.ipynb**: Download DailyDialog, generate Llama 3 summaries via Ollama.
   - **02\_finetune\_bart.ipynb**: Fine‑tune BART‑Large‑XSum on the custom dataset with PEFT/LoRA.
   - **03\_evaluate\_and\_chatbot.ipynb**: Evaluate pre‑ and post‑finetuning metrics (ROUGE, METEOR, BERTScore) and launch an interactive chatbot using the summarizer + DialoGPT.
   - code to load model is provided in the notebook

4.

   Enter your message at the prompt and watch the summary‑driven chatbot respond in real time!

---

## 📑 Notebooks Details

- **01\_data\_preparation.ipynb**\
  • Imports the DailyDialog dataset using `datasets`.\
  • Preprocesses dialogues and formats them for summarization.\
  • Uses Ollama’s Llama 3 endpoint to generate “gold” summaries for 2,000 conversations.

- **02\_finetune\_bart.ipynb**\
  • Loads `facebook/bart-large-xsum` and applies LoRA adapters (via `peft`).\
  • Fine‑tunes only adapter layers on the synthetic summaries.\
  • Saves the final adapter checkpoint under `model/checkpoint-2430/`.

- **03\_evaluate\_and\_chatbot.ipynb**\
  • Computes evaluation metrics (ROUGE‑1/2/L, METEOR, BERTScore) before vs. after fine‑tuning.\
  • Demonstrates an end‑to‑end chat loop:  summarize → condition DialoGPT → generate.

---

## 🛠 Requirements

```text
python>=3.8
transformers>=4.30.0
datasets
peft
ollama        # to run Llama 3 locally
rouge_score
meteor_score
bert-score
diffusers    # if needed for other tasks
```

Install everything via:

```bash
pip install -r requirements.txt
```

---

## 🔧 Usage Example

```
User: Hi there!
Bot: Hello! How can I assist you today?
User: Tell me a joke.
Bot: Why did the scarecrow win an award? Because he was outstanding in his field! 
```

---

## 📊 Evaluation Results

| Metric    | Before Fine‑tuning | After Fine‑tuning |
| --------- | ------------------ | ----------------- |
| ROUGE‑1   | 0.17               | 0.42              |
| ROUGE‑2   | 0.033              | 0.12              |
| ROUGE‑L   | 0.13               | 0.32              |
| METEOR    | 0.17               | 0.38              |
| BERTScore | 0.43               | 0.64             |

*(Values are illustrative—see ********************************************************************************`03_evaluate_and_chatbot.ipynb`******************************************************************************** for exact numbers.)*

---


## 🤝 Contributing

Contributions and issues are welcome! Please open a GitHub issue or pull request.

---

## 📜 License

This project is released under the Apache License. See `LICENSE` for details.

---

*Happy summarizing & chatting!*

