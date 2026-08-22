I just wrapped up my Machine Learning & AI Fluency Capstone with FlyRank! 🚀

For the past 8 weeks, I’ve been building an end-to-end ML pipeline that predicts organic search traffic decay for enterprise websites. 

One of the biggest technical decisions I made was ripping out my Pandas data ingestion loops and replacing them with vectorized DuckDB SQL views. This shift took my feature engineering compute time from 84.3 seconds down to 1.4 seconds, proving that model architecture doesn't matter if your data engine can't scale.

I also had to face a hard limitation: while my Gradient Boosted model achieved an honest 0.8215 ROC-AUC on unseen domains, it only measures correlative decay. It cannot predict unannounced Google algorithm updates. Because of that limitation, I designed the pipeline to output an advisory "Content Action Playbook" for human editors, rather than trying to build a fully autonomous AI CMS writer. 

Check out the full live research paper, interactive data architecture, and source code on my portfolio here: https://rafayyk7.github.io/flyrank-ml/
