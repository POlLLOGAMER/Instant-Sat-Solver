import random
import matplotlib.pyplot as plt

# Define the logical functions
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
    for _ in range(num_clauses):
        clause = [random.choice([1, 0]) for _ in range(num_variables)]
        clauses.append(clause)
    return clauses

# Function to evaluate the clauses with the current variables
def evaluate_clause(variables, clauses):
    results = []
    for clause in clauses:
        result = False
        for i, var in enumerate(clause):
            if var == 1:
                result = result or variables[i]  # Use the direct value of the variable
            else:
                result = result or (1 - variables[i])  # Use the inverted value of the variable
        results.append(result)
    return results

# Function to invert the variables
def invert_variables(variables):
    return [1 - var for var in variables]

# Function to check if the SAT is solved
def is_solved(variables, clauses):
    return all(evaluate_clause(variables, clauses))

# Test parameters
iterations = 100

# Data for plotting
variable_counts = list(range(1, 201, 10))  # Incrementing by 10
probabilities = []

# Run the simulation for different numbers of variables
for num_variables in variable_counts:
    num_clauses = num_variables  # Set the number of clauses equal to the number of variables
    successful_solutions = 0

    for _ in range(iterations):
        clauses = generate_random_sat_problem(num_variables, num_clauses)
        variables = [random.randint(0, 1) for _ in range(num_variables)]

        # Evaluate if the variables solve the SAT
        if is_solved(variables, clauses):
            successful_solutions += 1
        else:
            variables_inverted = invert_variables(variables)
            if is_solved(variables_inverted, clauses):
                successful_solutions += 1

    # Calculate probability and convert to percentage
    probability = (successful_solutions / iterations) * 100
    probabilities.append(probability)

# Plot
plt.plot(variable_counts, probabilities, marker='o', color='b')
plt.title("Accuracy Probability vs Number of Variables (Clauses equal to variables)")
plt.xlabel("Number of variables")
plt.ylabel("Accuracy probability (%)")
plt.grid(True)

# Show the plot without labels on the points
plt.show()
