# Loan Qualifier Application

### This is a command-line interface (CLI) application for finding qualifying loans for users, if any, based on the following variables of the user: credit score, debt, income, loan amount, and home value. The new functionality that was added was to prompt the user to save the list of qualifying loans into a new csv file.

---

## Technologies

This project leverages python 3.7 with the following packages:

- [fire](https://github.com/google/python-fire) - For the command line interface, help page, and entry-point.

- [questionary](https://github.com/tmbo/questionary) - For interactive user prompts and dialogs

---

## Installation Guide

Before running the application first install the following dependencies.

```python
  pip install fire
  pip install questionary
```

---

## Usage

To use the loan qualifier application simply clone the repository and run the **app.py** and input user information as prompted.

Key financial calculators that were used to determine if the user is qualified for any loans:

![Loan Qualifier CLI](Desktop/financial_calculators.png)

If the user is not qualified for any loans, the application will notify the user that

> "No loans have been found. You have exited the application."

If the user is qualified, the application will save the file as a csv andnotify the user that

> "You have successfully exited the application."

Below are the main functions that were used to prompt the user to save the list of loans into a new csv file:

```python
def save_qualifying_loans(qualifying_loans):
    """Saves the qualifying loans to a CSV file.

    Args:
        qualifying_loans (list of lists): The qualifying bank loans.
    """

    # if no qualifying loans have been found, then prompt user to exit
    if not qualifying_loans:
        sys.exit("No loans have been found. You have exited the application.")

    saveFile = questionary.confirm("Would you like to save the qualifying loans?").ask()

    # if qualifying loans have been found, and user wants to save file as CSV
    if saveFile:
        save_csv(qualifying_loans)
    else:
        sys.exit("You have successfully exited the application.")


def save_csv(qualifying_loans):
    header = ["Lender","Max Loan Amount", "Max LTV", "Max DTI", "Min Credit Score","Interest Rate"]
    csv_path = Path("./data/qualifying_loans.csv")
    with open(csv_path, "w") as csvfile:
        csvwriter = csv.writer(csvfile)
        csvwriter.writerow(header)
        csvwriter.writerows(qualifying_loans)

```
