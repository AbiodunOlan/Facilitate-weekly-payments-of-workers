# Facilitate-weekly-payments-of-workers/ Worker Payment Slip Generator

# PYTHON PROGRAMMING
Worker Payment Slip Generator
Description
This Python program generates weekly payment slips for a list of workers. Each worker has attributes such as ID, name, hourly wage, hours worked per week, and gender. The program calculates the weekly payment for each worker and assigns an employee level based on specific conditions. It then prints out the payment slips for each worker.

# Features
Generates a dynamic list of 400 workers with random attributes.
Calculates weekly payments based on hourly wage and hours worked.
Assigns employee levels based on salary and gender conditions.
Provides exception handling to manage potential errors gracefully.
# Requirements
Python 3.6 or higher
# Installation
Ensure you have Python installed on your system. 


# Python Code

import random

# Step 1: Define the structure of a worker
class Worker:
    def __init__(self, worker_id, name, hourly_wage, hours_worked_per_week, gender):
        self.worker_id = worker_id
        self.name = name
        self.hourly_wage = hourly_wage
        self.hours_worked_per_week = hours_worked_per_week
        self.gender = gender
    
    def compute_weekly_payment(self):
        return self.hourly_wage * self.hours_worked_per_week
    
    def determine_employee_level(self, weekly_payment):
        if 10000 < weekly_payment < 20000:
            return "A1"
        elif 7500 < weekly_payment < 30000 and self.gender == 'Female':
            return "A5-F"
        else:
            return "Unknown"

# Step 2: Create a function to generate a list of workers
def generate_workers(num_workers=400):
    workers = []
    genders = ['Male', 'Female']  # Assuming two genders for simplicity
    try:
        for i in range(1, num_workers + 1):
            worker_id = f"W{i:04d}"  # Generates worker IDs like W0001, W0002, ...
            name = f"Worker{i}"
            hourly_wage = random.uniform(15.0, 30.0)  # Random hourly wage between $15 and $30
            hours_worked_per_week = random.randint(350, 500)  # Random hours worked per week between 35 and 50
            gender = random.choice(genders)
            workers.append(Worker(worker_id, name, hourly_wage, hours_worked_per_week, gender))
    except Exception as e:
        print(f"Error occurred while generating workers: {str(e)}")
    return workers

# Step 3: Function to generate payment slips
def generate_payment_slips(workers):
    try:
        for worker in workers:
            weekly_payment = worker.compute_weekly_payment()
            employee_level = worker.determine_employee_level(weekly_payment)
            print(f"Worker ID: {worker.worker_id}, Name: {worker.name}, Weekly Payment: ${weekly_payment:.2f}, Employee Level: {employee_level}")
    except Exception as e:
        print(f"Error occurred while generating payment slips: {str(e)}")

# Generate the list of workers
workers_list = generate_workers()

# Generate payment slips for each worker
generate_payment_slips(workers_list)


# R PROGRAMMING
Facilitate the weekly payments of workers
Worker Payment Slip Generator

# Description
The R program generates weekly payment slips for a list of workers. Each worker has attributes such as ID, name, hourly wage, hours worked per week, and gender. The program calculates the weekly payment for each worker and assigns an employee level based on specific conditions. It then prints out the payment slips for each worker.

# Features
Generates a dynamic list of 400 workers with random attributes.
Calculates weekly payments based on hourly wage and hours worked.
Assigns employee levels based on salary and gender conditions.
Provides exception handling to manage potential errors gracefully.

# Requirements
R version 3.6 or higher
R6 package

# Installation
Ensure one have R installed on the system. one can download it from CRAN.
Install the R6 package if  haven't already:


Copy code
# Load necessary library
library(R6)

# Define Worker class using R6
Worker <- R6Class(
  "Worker",
  public = list(
    worker_id = NULL,
    name = NULL,
    hourly_wage = NULL,
    hours_worked_per_week = NULL,
    gender = NULL,
    initialize = function(worker_id, name, hourly_wage, hours_worked_per_week, gender) {
      self$worker_id <- worker_id
      self$name <- name
      self$hourly_wage <- hourly_wage
      self$hours_worked_per_week <- hours_worked_per_week
      self$gender <- gender
    },
    compute_weekly_payment = function() {
      return(self$hourly_wage * self$hours_worked_per_week)
    },
    determine_employee_level = function(weekly_payment) {
      if (weekly_payment > 10000 & weekly_payment < 20000) {
        return("A1")
      } else if (weekly_payment > 7500 & weekly_payment < 30000 & self$gender == "Female") {
        return("A5-F")
      } else {
        return("Unknown")
      }
    }
  )
)

# Function to generate a list of workers
generate_workers <- function(num_workers = 400) {
  genders <- c("Male", "Female")
  workers <- list()
  try({
    for (i in 1:num_workers) {
      worker_id <- paste0("W", sprintf("%04d", i))
      name <- paste0("Worker", i)
      hourly_wage <- runif(1, 15, 30)  # Random hourly wage between $15 and $30
      hours_worked_per_week <- sample(35:50, 1)  # Random hours worked per week between 35 and 50
      gender <- sample(genders, 1)  # Random gender assignment
      workers[[i]] <- Worker$new(worker_id, name, hourly_wage, hours_worked_per_week, gender)
    }
  }, silent = TRUE)
  return(workers)
}

# Function to generate payment slips
generate_payment_slips <- function(workers) {
  try({
    for (worker in workers) {
      weekly_payment <- worker$compute_weekly_payment()
      employee_level <- worker$determine_employee_level(weekly_payment)
      cat(sprintf("Worker ID: %s, Name: %s, Weekly Payment: $%.2f, Employee Level: %s\n",
                  worker$worker_id, worker$name, weekly_payment, employee_level))
    }
  }, silent = TRUE)
}

# Generate workers
workers_list <- generate_workers()

# Generate payment slips
generate_payment_slips(workers_list)
