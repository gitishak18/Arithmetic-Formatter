# Arithmetic-Formatter
def arithmetic_arranger(problems, show_answers=False):
    # Check if there are too many problems (more than 5)
    if len(problems) > 5:
        return "Error: Too many problems."

    # Initialize empty lists for each row of the arranged problems
    top_row = []
    bottom_row = []
    lines = []
    results = []

    # Loop through each problem in the list
    for problem in problems:
        # Split the problem into the operands and the operator
        operands = problem.split()
        operator = operands[1]

        # Check if the operator is valid
        if operator not in ['+', '-']:
            return "Error: Operator must be '+' or '-'."

        # Check if the operands are valid (consist of digits only)
        if not operands[0].isdigit() or not operands[2].isdigit():
            return "Error: Numbers must only contain digits."

        # Get the length of the longest operand
        operand_length = max(len(operands[0]), len(operands[2]))

        # Add spaces to the left of the operands to make them the same length
        top_operand = operands[0].rjust(operand_length + 2)
        bottom_operand = operator + operands[2].rjust(operand_length + 1)

        # Add the operands and the line below them to the appropriate list
        top_row.append(top_operand)
        bottom_row.append(bottom_operand)
        lines.append('-' * (operand_length + 2))

        # If the show_answers flag is True, calculate the result and add it to the results list
        if show_answers:
            result = str(eval(problem)).rjust(operand_length + 2)
            results.append(result)

    # Combine the rows into a single string
    arranged_problems = '    '.join(top_row) + '\n' + '    '.join(bottom_row) + '\n' + '    '.join(lines)

    # If the show_answers flag is True, add the results to the end of the arranged problems
    if show_answers:
        arranged_problems += '\n' + '    '.join(results)

    # Return the arranged problems
    return arranged_problems
