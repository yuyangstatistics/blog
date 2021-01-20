---
title: Paper Reading -- A Survey on Machine Reading Comprehension by Zeng et al. 2020
date: 2021-01-19 19:51:00 -0500
categories: [NLP, MRC]
tags: [paper, mrc]
---

[A Survey on Machine Reading Comprehension: Tasks, Evaluation Metrics, and Benchmark Datasets](https://arxiv.org/abs/2006.11880)

This paper provides a comprehensive survey on MRC tasks, evaluation metrics, and existing benchmark datasets. I find the *Tasks* section and the *Open Issues* section most helpful. 

-----------------

In the *Tasks* section, 
1. a definition of typical MRC tasks is given, which can be seen as a supervised problem: (context, question -> answer).
2. concept clarification about MRC
    - multi-modal MRC vs. textual MRC: multi-modal MRC also involves images and videos, such as RecipeQA and MovieQA.
    - MRC vs. QA: 
        - These two tasks are not subsets of one another. 
        - Some MRC may be seen as a special case QA, in that QA can also be open-domain and that QA can also be solved by rule-based method, information retrival method and knowledge-based method.
        - On the other hand, just like human, reading comhension can be about giving correct answers to questions, and can also be about asking the right or sensible questions given the context. And in multi-modal MRC, QA is just one part of it, and we also need CV.
    - MRC vs. NLP. Syntax information can help with MT, and some MRC models can be used in NLI as well (ex. SAN). (Need to figure out the definitions of NLP and NLI.)
3. Classification of MRC Tasks (clear and well-defined)
    - type of corpus: multi-modal, textual
    - type of questions: cloze style, natural, synthetic
    - type of answers: natural, multiple choice
    - source of answers: span, free-form

-----------------

In the *Benchmark Dataset* section, the authors list almost all available datasets and they kindly provide a website summarizing all the datasets. One good feature I like the most is the prerequisite skills (Table 8) and an overview of the characterisitcs of each dataset (Table 10). The prerequisite skills may provide some ideas on building new models and interpretation. And among the characteristics, I am the most interested in *Complex Reasoning*.

I checked most of them and found that some of them were not active in these two years. I hereby list the ones that I find active and interesting and also with leaderboard. I care about leaderboard is because I want to check the gap between the state-of-art of human performance to see further improvement potential.

- [ARC](https://leaderboard.allenai.org/arc/submissions/public): commonsense knowledge and complex reasoning
- [OpenBookQA](https://leaderboard.allenai.org/open_book_qa/submissions/public): commonsense knowledge
- [ReCoRD](https://sheng-z.github.io/ReCoRD-explorer/)  (part of SuperGLUE now): commonsense knowledge
- [HotpotQA](https://hotpotqa.github.io)
- [SciTail](https://leaderboard.allenai.org/scitail/submissions/public)
- [DROP](https://leaderboard.allenai.org/drop/submissions/public): complex reasonsing
- [RACE](http://www.qizhexie.com/data/RACE_leaderboard.html): passage reading comprehension from middle- and high-school English exams. Involve complex reasoning. I am intersted in this dataset since the questions in the exams are usually made up by experts and should have higher quality.
- [TriviaQA](https://competitions.codalab.org/competitions/17208#results)
- [SQuAD](https://rajpurkar.github.io/SQuAD-explorer/)
- [CoQA](https://stanfordnlp.github.io/coqa/): conversational QA
- [SuperGLUE](https://super.gluebenchmark.com/leaderboard)

-------------

In the *Open Issues* section, the authors think multi-modal MRC, commonsense knowledge, complex reasoning, robustness, and interpretability is worth investigation. And I am interested in commonse knowledge and complex reasoning.


-------------

### References
[1] Zeng, Chengchang, et al. "A Survey on Machine Reading Comprehension: Tasks, Evaluation Metrics, and Benchmark Datasets." arXiv preprint arXiv:2006.11880 (2020). 
```
@article{zeng2020survey,
  title={A Survey on Machine Reading Comprehension: Tasks, Evaluation Metrics, and Benchmark Datasets},
  author={Zeng, Chengchang and Li, Shaobo and Li, Qin and Hu, Jie and Hu, Jianjun},
  journal={arXiv preprint arXiv:2006.11880},
  year={2020}
}
```