# LiHuaVerse: A Multimodal Conversational Benchmark for Retrieval-Augmented Generation  

## Overview  
**LiHuaVerse** is a synthetic benchmark dataset for evaluating **retrieval-augmented generation (RAG)** systems in multimodal conversational question-answering contexts.  
It extends the original [LiHua-World](https://github.com/HKUDS/MiniRAG/tree/main/dataset/LiHua-World) text-only benchmark by introducing **synthetic images** and **additional multimodal question–answer pairs**, further simulating the complexity of real-world instant messaging.  

LiHuaVerse is designed to test:  
- **Multimodal retrieval** (text + images).  
- **Multi-hop reasoning** across conversations.  
- **End-to-end RAG pipelines** in realistic settings.  

All conversations and images are **synthetically generated** to preserve privacy while maintaining contextual realism.  

---

## Key Features  
- **425 conversations** spanning a simulated **52-week timeline**.  
- **398 synthetic images** embedded directly in dialogue contexts.  
- **1,078 question–answer pairs** (expanded from 637 in LiHua-World).  
  - Includes **single-hop** and **multi-hop** multimodal QA.  
  - Questions require reasoning over both **textual and visual elements**.  
- **Difficulty annotation** (easy / medium / hard) based on model evaluation scores.  
- **Metadata** linking questions to relevant conversational documents and images.  
- Compatible with **RAG pipelines**, multimodal LLMs, and retrieval system evaluations.  

---

## 📊 Benchmark Results  

The following table reports baseline results on **LiHuaVerse** using a range of vision–language models (VLLMs) with *k = 3* retrieved documents.  

| Model                  | BERTScore F1 | ROUGE-L F1 | CIDEr-D | LAVE | Mixture of Judges | Composite Score |
|------------------------|--------------|------------|---------|------|-------------------|-----------------|
| **Gemma-3 (12B)**      | 0.154        | 0.189      | 0.579   | 0.676 | 0.606             | 0.399           |
| **Gemma-3 (4B)**       | 0.143        | 0.173      | 0.494   | 0.641 | 0.560             | 0.363           |
| **Pixtral-2409 (12B)** | 0.207        | 0.218      | 0.824   | 0.761 | 0.663             | 0.503           |
| **Qwen2.5-VL (3B)**    | 0.167        | 0.190      | 0.623   | 0.710 | 0.558             | 0.422           |
| **Qwen2.5-VL (7B)**    | 0.195        | 0.209      | 0.698   | 0.812 | 0.692             | 0.479           |
| **Qwen2.5-VL (32B)**   | 0.194        | 0.222      | 0.749   | 0.818 | 0.712             | 0.496           |

> **Note**: Composite Score is the normalized mean across metrics (BERTScore, ROUGE-L, CIDEr-D, and LAVE).  

---

## File Structure  
```
LiHuaVerse/
│
├── data
│   ├── conversations/            # text files of augmented conversations
│   │   ├── week1
│   │   │   ├── 20260105_1100.txt
│   │   │   ├── 20260105_1400.txt
│   │   │   └── ...
│   │   ├── week2
│   │   │   ├── 20260112_1000.txt
│   │   │   ├── 20260112_1500.txt
│   │   │   └── ...
│   │   └── ...
│   │
│   ├── images/                   # Synthetic images aligned to conversations
│   │   ├── week1
│   │   │   ├── 20260105_1100.jpg
│   │   │   ├── 20260105_1400.jpg
│   │   │   └── ...
│   │   ├── week2
│   │   │   ├── 20260112_1000.jpg
│   │   │   ├── 20260112_1500.jpg
│   │   │   └── ...
│   │   └── ...
│   │
│   └── questions/                # Question–answer in .csv and .json format
│       ├── query_set.csv
│       ├── query_set.json
│
├── notebooks                     # Some of the notebooks used to create and evaluate the data
│   │   ├── augmented_conversations_eval.ipynb
│   │   ├── dalle_image_gen.ipynb
│   │   └── ...
│
└── README.md                 # This file
```

---

## Data Format  

### Conversations (`conversations/*.txt`)  
Each file contains one augmented conversation with inline image references.  
```
Time: 20260105_11:00
LiHua: Hey! Just wanted to let you know that I’ve arrived in the city! 🎉 How about we grab lunch together on the day after tomorrow, the 8th? Let me know what works for you! 😊
WolfgangSchulz: Awesome! Can't wait to catch up. I'll look for a nice spot for us to hang out. See you on the 8th! 🎶✨  
LiHua: Perfect! I'm looking forward to it! Let’s make it a fun day! 😄  
WolfgangSchulz: Definitely! It's been too long. We're going to have such a great time! 🎉 By the way, check this out—here’s a photo I took of the riverside café I’m thinking about for our lunch.  
*WolfgangSchulz: [shared image: 20260105_1100.jpg]  
LiHua: Wow, that looks beautiful! I love the view—can't wait to catch up there!

```

### Question–Answer Pairs (`qa_pairs.jsonl`)  
Each QA pair is linked to the relevant date/time.  
```
{
  "question": "What flavor was the protein powder Li Hua tried?",
  "answer": "Vanilla flavor with no added sugar and 24g of protein per serving.",
  "evidence": ["20260204_1500"],
  "difficulty": "hard"
}
```
---

## Limitations  
- **Modalities**: Only text and images are included. Audio and video remain excluded.  
- **Character consistency**: Visual depictions of Li Hua may vary across images.  
- **Conversational realism**: Lacks natural imperfections such as typos, slang, or selfies.  
- **Evaluation**: Current judge-based scoring is limited in capturing partial correctness.  

---

## Citation  
If you use LiHuaVerse in your work, please cite:  

```
@mastersthesis{nichollsconversationragbenchmark,
  title={Toward Realistic Evaluation of Multimodal Retrieval-Augmented Generation Systems},
  author={Robin Nicholls},
  year={2025},
  school={Univeristy of Edinburgh}
}
```

---

## License  
LiHuaVerse is released under the **MIT License**. All content (including images) is synthetically generated.  
