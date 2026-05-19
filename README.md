# Viterbi Algorithm Implementation for Hidden Markov Models

A comprehensive implementation of the Viterbi algorithm for finding the most likely sequence of hidden states in a Hidden Markov Model (HMM), applied to genomic sequence analysis.

## Overview

This project demonstrates the Viterbi algorithm, a dynamic programming approach to solve the decoding problem in Hidden Markov Models. The implementation uses genomic sequences as an example, identifying hidden states (exons, introns, splice sites, etc.) from observed DNA nucleotide sequences.

## Features

- **Viterbi Algorithm**: Efficient dynamic programming implementation to find the maximum likelihood path through an HMM
- **Log-scale Probability Calculations**: Uses log probabilities to avoid numerical underflow issues
- **Trace-back Mechanism**: Reconstructs the optimal state sequence from the Viterbi matrices
- **Genomic Application**: Configured with biological transition and emission probabilities for DNA sequence analysis

## Project Structure

- `ViterbiHMM.ipynb` - Main Jupyter notebook containing:
  - Model configuration (states and probabilities)
  - Viterbi algorithm implementation
  - Test cases with various state paths
  - Visualization of the Viterbi matrix

## Model Configuration

### Hidden States
- `s` - Start state
- `E` - Exon (protein-coding region)
- `5` - 5' splice site
- `I` - Intron (non-coding region)
- `e` - End state

### States and Transitions

The model includes:
- **State Transition Probabilities**: Defined as a 5×5 matrix specifying the probability of transitioning from one state to another
- **Emission Probabilities**: Define the likelihood of observing each nucleotide (A, C, G, T) in each state

## Key Functions

### `setup_viterbi(query_sequence)`
Initializes the Viterbi value and trace matrices for a given sequence.
- Creates a matrix of dimensions (num_states × seq_len)
- Fills the first column based on initial state and emission probabilities
- Initializes the trace matrix for backtracking

### `viterbi_forward(query_sequence, viterbi_value_matrix, viterbi_trace_matrix)`
Performs the forward pass of the Viterbi algorithm.
- Iterates through each position in the sequence
- For each state, calculates the maximum probability path from previous states
- Stores the best previous state for trace-back

### `traceback_best_state_path(viterbi_value_matrix, viterbi_trace_matrix)`
Reconstructs the optimal state sequence.
- Finds the state with the highest probability at the sequence end
- Traces back through the trace matrix to build the complete path
- Converts state indices to state names

### `get_log_prob_for_state_path(state_path, query_sequence)`
Calculates the log probability for a given state path and sequence combination.

## Example Usage

```python
# Setup and run Viterbi algorithm
viterbi_value_matrix, viterbi_trace_matrix = setup_viterbi(query_sequence)
viterbi_forward(query_sequence, viterbi_value_matrix, viterbi_trace_matrix)
best_state_path = traceback_best_state_path(viterbi_value_matrix, viterbi_trace_matrix)

print(best_state_path)
# Output: ['E', 'E', 'E', ..., 'E'] (most likely state sequence)
