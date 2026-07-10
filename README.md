# Loan Management System

A small Django-based loan management application that provides user registration, loan application, loan approval, and EMI/payment tracking.

## Features

- Multi-step user registration with file uploads (profile, Aadhaar, PAN, signature)
- Field validations (Aadhaar 12 digits, PAN format, IFSC format, account number length)
- Loan application and approval workflow
- Payment / EMI tracking

## Requirements

- Python 3.8+ (this project was developed with Python 3.13.x)
- Django (see `settings.py` for version used; `Django==5.0.2` in local environment)
- A database (MySQL is configured in `loan_project/settings.py` in this workspace)
- Pillow (for image fields)

## Quick setup

1. Clone the repository (if not already):

   git clone https://github.com/<your-username>/<repo>.git
   cd loan_project-main

2. Create and activate a virtual environment:

   # Windows
   python -m venv venv
   venv\Scripts\activate

   # macOS / Linux
   python3 -m venv venv
   source venv/bin/activate

3. Install dependencies:

   pip install -r requirements.txt

   If you don't have a `requirements.txt`, install at least:

   pip install Django Pillow mysqlclient

4. Configure database and environment

   - Update `loan_project/settings.py` with your DB credentials (or set environment variables).
   - Ensure `MEDIA_ROOT` points to `media/` and `MEDIA_URL` is configured (already present in settings in this project).

5. Run migrations and create a superuser:

   python manage.py makemigrations
   python manage.py migrate
   python manage.py createsuperuser

6. Run the development server:

   python manage.py runserver

   Open http://127.0.0.1:8000/ in your browser.

## Important files & notes

- `loan_app/models.py` — data models (AccountHolder, LoanApplication, LoanApproval, Payment)
- `loan_app/views.py` — views and registration logic (includes server-side validation for DOB, Aadhaar, PAN, IFSC, account number)
- `templates/register.html` — multi-step registration form with client-side validation
- `media/` — folder for uploaded images (profile, aadhaar, pan, signature)

## Validation rules implemented

- Aadhaar: exactly 12 numeric digits (spaces removed on submit)
- PAN: 5 letters, 4 digits, 1 letter (e.g. `ABCDE1234F`) — validated client- and server-side
- IFSC: 11 characters — 4 letters, `0`, 6 alphanumeric (e.g. `SBIN0012345`)
- Account number: 9–18 digits
- Date of birth: required and parsed as `YYYY-MM-DD`

## Running tests

- There are no automated tests included yet. To add tests, implement tests in `loan_app/tests.py` and run:

  python manage.py test

## Contributing

- Fork the repo, create a feature branch, and open a pull request.
- Add tests for new functionality and keep code formatting consistent.

## License

Include a license if you want to open-source this project. For private/internal projects you can skip this step.

---

If you want, I can also:
- generate `requirements.txt` from your environment,
- add a simple `docker-compose.yml` for local dev, or
- create basic unit tests for the registration validations.
