# Whiteboard
This is a virtual whiteboard for me to flesh out some ideas I've had that may or may not be work well and make good starting points for research. The idea is that eventually I will get around to putting them to the test or realizing that they won't actually work. If you've got a similar idea, think of some challenges I might run into or something that I'm overlooking, or want to work together, feel free to open an issue, submit a pull request, or get in tough.

## Categories

[Causal Discovery](#causal-discovery)

[Reinforcement Learning](#reinforcement-learning)

[Game Theory and Other Sequential Decisionmaking Formalizations](#game-theory-and-other-sequential-decisionmaking-formalizations)

## Causal Discovery

### Causal Discovery as a Bandit Problem
1. The challenge of structure learning is the number of possible DAGs and the number of data points for calculating scores or independence tests
    1. One way to solve the second problem is to run the independence tests or score functions on a random subset of the data many times
        1. If the sampling is independent, then in theory the average of these smaller calculations should converge to the score or test statistics for the whole dataset
    2. Causal Discovery as a bandit problem to avoid enumerating over every DAG
        1. Balance exploration of best known DAG with exploitation of unknown DAGS
        2. Can consider each DAG as an arm in a MAB and use CI tests or score fucntions on subsets of data as rewards
        3. Too many to enumerate, so need some algorithm for infinitely-armed bandits
            1. One potential is GP
            2. There are other algorithms out there, I just need to look more into it
            3. Could then probably use UCB, TS, or some minimal regret acquisition function
        4. How to convert DAGs to unique arms
            1. Need to map each DAG to unique number to get arm IDs
            2. Don't want to build every DAG and assign a number
                1. Takes too much time and memory
                2. Need a bijection from DAGs to integers without constructing the DAG explicitly, only if we pull that arm to calculate reward
                    1. Adjacency matrix of DAG is lower triangular 1s and 0s
                    2. If entry is not 1, it is 0 so really only need to focus on one or the other
                    3. Each 1 in lower triangular adjacency matrix corresponds to unique row and column in the matrix
                    4. Go row by row and concatenate number (row column) for each 1 in matrix
                    5. Creates unique integer for each DAG
                    6. Can enumerate over these integers without explicitly constructing DAGs or adjacency matrices
    5. With arm IDs and way to calculate (stochastic) rewards each time we pull an arm (DAG), we can use bandit algorithm to find the best arm!
  
### Causal Discovery via MCMC
1. Same approach as above to calculating scores or independence tests
2. Same approach for assigning unique numbers to DAGs
3. Use Hamiltonian MCMC to sample over graphs
    1. Ideally want to make it converge faster
        1. Maybe use temperature schedule
        2. Could also use some kind of exploration bonus
            1. Want to encourage exploration early on but quicly converge to the best DAG(s)
                1. Maybe use active learning or similar approach to Ready Policy One paper

## Reinforcement Learning

## Game Theory and Other Sequential Decision-making Formalizations
