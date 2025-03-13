IIT BHU(WORKSHOP) CALCULATOR CODE
<br>
import math
import cmath  # For complex number calculations
import sympy  as sy # For algebra and calculus
import gradio  as gr # For UI

# History tracking list
history = []

def add_to_history(operation, result):
    """Adds a performed calculation to the history list."""
    history.append(f"{operation} = {result}")

def show_history():
    """Returns the history of all calculations performed."""
    return "\n".join(history) if history else "No calculations yet!"

# Arithmetic Operations
def addition(a, b):
    result = a + b
    add_to_history(f"{a} + {b}", result)
    return result

def subtraction(a, b):
    result = a - b
    add_to_history(f"{a} - {b}", result)
    return result

def multiplication(a, b):
    result = a * b
    add_to_history(f"{a} * {b}", result)
    return result

def division(a, b):
    if b == 0:
        return "Error: Division by zero is not allowed."
    result = a / b
    add_to_history(f"{a} / {b}", result)
    return result

# Algebra Functions
def quadratic_roots(a, b, c):
    discriminant = cmath.sqrt(b**2 - 4*a*c)
    root1 = (-b + discriminant) / (2 * a)
    root2 = (-b - discriminant) / (2 * a)
    add_to_history(f"Roots of {a}x^2 + {b}x + {c}", (root1, root2))
    return root1, root2

# Trigonometry
def sine(angle):
    result = math.sin(math.radians(angle))
    add_to_history(f"sin({angle})", result)
    return result

def cosine(angle):
    result = math.cos(math.radians(angle))
    add_to_history(f"cos({angle})", result)
    return result

def tangent(angle):
    result = math.tan(math.radians(angle))
    add_to_history(f"tan({angle})", result)
    return result

# UI with Gradio
def calculate(operation, a, b=None, c=None):
    if operation == "Addition":
        return addition(a, b)
    elif operation == "Subtraction":
        return subtraction(a, b)
    elif operation == "Multiplication":
        return multiplication(a, b)
    elif operation == "Division":
        return division(a, b)
    elif operation == "Quadratic Roots":
        return quadratic_roots(a, b, c)
    elif operation == "Sine":
        return sine(a)
    elif operation == "Cosine":
        return cosine(a)
    elif operation == "Tangent":
        return tangent(a)
    else:
        return "Invalid Operation"

with gr.Blocks() as demo:
    gr.Markdown("# Advanced Calculator")
    
    operation = gr.Dropdown([
        "Addition", "Subtraction", "Multiplication", "Division",
        "Quadratic Roots", "Sine", "Cosine", "Tangent"
    ], label="Select Operation")
    
    a = gr.Number(label="First Input")
    b = gr.Number(label="Second Input (Optional)", optional=True)
    c = gr.Number(label="Third Input (Optional, for Quadratic Roots)", optional=True)
    
    result_btn = gr.Button("Calculate")
    result_output = gr.Textbox(label="Result")
    
    history_btn = gr.Button("Show History")
    history_output = gr.Textbox(label="Calculation History")
    
    result_btn.click(calculate, inputs=[operation, a, b, c], outputs=result_output)
    history_btn.click(show_history, inputs=[], outputs=history_output)

demo.launch()

