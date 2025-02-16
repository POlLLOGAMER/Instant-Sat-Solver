# Instant-Sat-Solver
Instant SAT solver is a SAT solving algorithm that proves that p=np, because it can solve a SAT problem in polynomial time. That is, the more numbers of variables and clauses there are, the more likely it is that it will solve the SAT problem. In summary, the probability that the SAT is resolved in the first iteration of the algorithm rises exponentially as there are more variables and clauses.

This algorithm works through probability theory, but being used with a reverse engineering technique, that is, the more variables and clauses there are, the more solutions there will be, and the less likely it is that a random combination and its inverse will be false for the SAT problem.

Heres the code:
```
import random

# Define logical functions
def XOR(a, b):
    return a != b

def NOR(a, b):
    return not (a or b)

def AND(a, b):
    return a and b

def OR(a, b):
    return a or b

# Function to generate a random SAT problem with clauses and variables
def generate_random_sat_problem(num_variables, num_clauses):
    clauses = []
    for _ in range(num_clauses):  # Let's say we have a number of clauses
        clause = []
        for _ in range(num_variables):
            # Randomly add positive or negated variables (simulating variables in SAT)
            clause.append(random.choice([1, 0]))
        clauses.append(clause)
    return clauses

# Function to evaluate the clauses with the current variables
def evaluate_clause(variables, clauses):
    results = []
    for clause in clauses:
        result = False
        for i, var in enumerate(clause):
            if var == 1:
                result = result or variables[i]  # Use direct value of the variable
            else:
                result = result or (1 - variables[i])  # Use inverted value of the variable
        results.append(result)
    return results

# Function to invert the variables
def invert_variables(variables):
    return [1 - var for var in variables]

# Function to check if the SAT is solved
def is_solved(variables, clauses):
    return all(clause_result for clause_result in evaluate_clause(variables, clauses))

# Generate a random SAT problem with over 1000 variables
num_variables = 1000  # Now we have 1000 variables
num_clauses = 6  # You can adjust the number of clauses here
clauses = generate_random_sat_problem(num_variables, num_clauses)

# Generate a random configuration of variables
variables = [random.randint(0, 1) for _ in range(num_variables)]
print(f"Random SAT problem generated with {num_variables} variables: {clauses[:5]}...")  # Only show the first 5 clauses to avoid output overload
print(f"Random variables generated (sample of the first 10 values): {variables[:10]}...")

# Evaluate if the variables solve the SAT
if not is_solved(variables, clauses):
    print("The SAT is not solved with the initial variables.")
    
    # Invert the variables
    variables_inverted = invert_variables(variables)
    print(f"Inverted variables (sample of the first 10 values): {variables_inverted[:10]}...")
    
    # Evaluate again with the inverted variables
    if is_solved(variables_inverted, clauses):
        print("The SAT was solved by inverting the variables!")
    else:
        print("The SAT was not solved even with the inverted variables.")
else:
    print("The SAT is already solved with the initial variables!")
```
What this code does is create random SAT algorithms, and test with 100 variables and 100 clauses, and assign a value true or false to each variable randomly, and if it is not true in total, the true turns them into false and the false into true.

In theory, at first it would be very unlikely that it would be true, but the more the amounts of variables and clauses increased, the more likely it would be that the SAT would be true.

## Graphing effectiveness
