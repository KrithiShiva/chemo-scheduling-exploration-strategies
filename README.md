# Performance Evaluation of Exploration Strategies in Double Q-Learning for Multi-Drug Chemotherapy Scheduling

A simulation study comparing three exploration strategies inside a Double Q-Learning framework for three-drug chemotherapy scheduling, using a pharmacokinetic–pharmacodynamic (PK/PD) tumour model.

> **Disclaimer:** This is a computational simulation for research and learning. It is not a clinical tool and must not be used for dosing or treatment decisions.

## Abstract

Optimising chemotherapy drug scheduling is a challenging sequential decision-making problem that requires balancing tumour suppression, drug toxicity and treatment resistance. Reinforcement Learning (RL) offers an adaptive approach to this problem. Alizade and Hajipour (2026) proposed a Double Q-Learning framework for three-drug chemotherapy optimisation using a PK/PD tumour model. However, the influence of different exploration–exploitation strategies on the learning performance of this framework remains unexplored.

This study investigates three exploration strategies: exponential decay ε-greedy, sigmoid decay ε-greedy and Upper Confidence Bound (UCB), within the Double Q-Learning framework. A Python-based chemotherapy simulation environment was reconstructed using eight tumour resistance compartments and three drugs: cisplatin, docetaxel and irinotecan. Each drug has seven discrete dosage levels, giving 343 possible action combinations. The strategies were evaluated over 100 training episodes across three random seeds.

Sigmoid decay ε-greedy achieved the highest mean reward during the final 20% of training and the lowest terminal tumour burden (70.8 cells). However, the reward differences were not statistically significant, and all strategies exceeded the predefined toxicity threshold. Limited state–action exploration further indicates insufficient training. Further training, statistical validation and improved toxicity control are needed before a reliable exploration strategy can be established for this application.

**Keywords:** Reinforcement Learning, Double Q-Learning, Exploration–Exploitation Trade-off, ε-Greedy, Sigmoid Decay, Upper Confidence Bound, Chemotherapy Scheduling, PK/PD Model

## Experimental setup

| Item | Value |
|---|---|
| Tumour model | 8 compartments (sensitive + resistant sub-populations) |
| Drugs | Cisplatin, Docetaxel, Irinotecan |
| Dose levels | 7 per drug (0, 5, 10, 20, 30, 40, 50) |
| Actions | 7³ = 343 |
| Treatment horizon | 84 days |
| Training | 100 episodes, 3 random seeds (11, 22, 33) |
| Learning rate (α) | 0.01 |
| Discount factor (γ) | 0.99 |
| Algorithm | Tabular Double Q-Learning |

### Exploration strategies compared

1. **Exponential decay ε-greedy**: ε decays from 1.0 to 0.01 (decay rate 0.995 per episode).
2. **Sigmoid decay ε-greedy**: ε follows a sigmoid curve, staying high early and dropping around the middle of training.
3. **Upper Confidence Bound (UCB)**: picks the action with the highest value estimate plus an uncertainty bonus (c = 1.5).

## Results (mean reward, final 20% of training)

| Strategy | Mean reward (± SD across seeds) |
|---|---|
| **Sigmoid decay ε-greedy** | **−15,761 ± 134** |
| UCB | −15,997 ± 290 |
| Exponential decay ε-greedy | −16,071 ± 228 |

- Sigmoid decay ε-greedy also reached the lowest terminal tumour burden (70.8 cells).
- Differences in reward were **not statistically significant**.
- All strategies **exceeded the toxicity threshold**.

## Limitations

- The simulator is a reconstruction from the paper's equations, not the authors' original code.
- State discretisation, reward aggregation and integration settings are implementation assumptions.
- With 343 actions, tabular learning covers only a small part of the state–action space after 100 episodes.
- Only 3 seeds were used, so statistical power is limited.
- Results are simulation-only.

## How to run

1. Clone the repository:
   ```bash
   git clone https://github.com/KrithiShiva/chemo-scheduling-exploration-strategies.git
   cd chemo-scheduling-exploration-strategies
   ```
2. Install the dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Open `double_q_learning_chemo.ipynb` in Jupyter or Google Colab and run all cells.
4. Results are saved to the `outputs/` folder as CSV files.

## Repository contents

| File | Description |
|---|---|
| `double_q_learning_chemo.ipynb` | Full implementation: simulator, Double Q-Learning agent, exploration strategies, plots |
| `requirements.txt` | Python dependencies |
| `outputs/` | CSV results (episode-level, seed-level, strategy summary, evaluation trajectories) |

## Reference

Alizade, B. & Hajipour, A. (2026). *Double Q-Learning for Intelligent Multi-Drug Scheduling in Cancer Chemotherapy Optimisation.* IET Systems Biology, 20:e70083. https://doi.org/10.1049/syb2.70083

## Author

Krithi Shiva · M.Sc. Data Science, SASTRA University
[GitHub](https://github.com/KrithiShiva) · [LinkedIn](https://linkedin.com/in/krithishiva)
