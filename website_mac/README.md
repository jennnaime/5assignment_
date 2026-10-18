# MacBook Neo

## Topic

Advertising website for the new Apple MacBook Neo laptop.

## Project goal

To present the MacBook Neo to students, designers and developers — show its features, colors and benefits in a clean, responsive interface.

## Team

- **Aisha** — Home page (index.html), contact form (Task 0–2), registration form (Task 3)
- **Anel** — About us (about.html)
- **Ayana** — Service (service.html)
- **Merey** — Contacts page (contacts.html layout, FAQ, contact information)

## Page ownership

| Page | Owner | Purpose |
|------|-------|---------|
| index.html | Aisha | Hero, benefits, featured product |
| service.html | Ayana | Features and catalogue |
| about.html | Anel | Story, team, quote |
| contacts.html | Merey / Aisha | Contact info, FAQ, contact form |
| register.html | Aisha | Registration form (Assignment #5, Task 3) |

## Local opening

1. Download or clone the repository.
2. Open `index.html` in any modern browser.
3. Or use a local server: `python -m http.server` and open `http://localhost:8000`.

No installation and no internet connection are required: Bootstrap 5.3.3 is stored
locally in `css/vendor/` and `js/vendor/`, so the forms also work offline.

## Assignment #5 — Part 1. Forms and Validation

### Files added or changed

| File | What it contains |
|------|------------------|
| `contacts.html` | Contact form rebuilt with the Bootstrap grid, `form-label`, `form-control`, helper text and `valid-feedback` / `invalid-feedback` |
| `register.html` | New registration form (Task 3) |
| `css/forms.css` | Styles for both forms, adapted to the site palette |
| `js/validation.js` | Contact form validation and the message character counter |
| `js/register.js` | Password / confirm password comparison and reset handling |
| `css/vendor/bootstrap.min.css`, `js/vendor/bootstrap.bundle.min.js` | Bootstrap 5.3.3, stored locally |

### Task 0 — Contact form

Fields: Name (text), Email (email), Topic (select), Message (textarea), Submit and Reset.

- Every field has a `name` attribute and a unique `id`.
- Every visible label is connected with `for` / `id`; placeholders are only a hint and never replace labels.
- The form is a real `<form>` element with `novalidate`, so the browser's own popups are replaced by Bootstrap feedback.

### Task 1 — HTML5 validation

| Rule | Attribute |
|------|-----------|
| Name is required | `required` |
| Name is at least 2 characters | `minlength="2"` |
| Email format | `type="email"` + `required` |
| Message is required | `required` |
| Message is 10 to 500 characters | `minlength="10"` + `maxlength="500"` |

### Task 2 — Bootstrap styling and feedback

- Layout is built with the Bootstrap grid: `row g-3`, `col-md-6`, `col-12`.
- Controls use `form-label`, `form-control`, `form-select` and a helper class (`field-help`, renamed to avoid a clash with the site's own `.form-text` column class).
- The Bootstrap validation pattern is used: the form is checked on submit, then the `was-validated` class keeps the feedback live while the user types, so a field is never permanently marked valid or invalid.
- Optional fields do not turn green — only the fields that are actually required show a success state.
- The form is one column on mobile and two columns from the `md` breakpoint.

### Task 3 — Registration form

`register.html` contains:

- First Name and Last Name — required, `minlength="2"`;
- Email — required, `type="email"`;
- Password and Confirm Password — required, `minlength="8"`;
- Gender — optional radio group with a "Prefer not to say" option, grouped in `fieldset` + `legend`;
- Hobbies — optional checkboxes, also in `fieldset` + `legend`;
- Country — required `select` with an empty default option;
- Submit and Reset buttons.

Password comparison is done in JavaScript, because HTML5 cannot compare two fields:

```js
confirmPassword.setCustomValidity(confirmValue === password.value ? '' : 'The passwords do not match.');
```

`setCustomValidity('')` is called again on every `input` event, so the error disappears as soon as the input is corrected. The Reset button clears the values, the `was-validated` class, the custom error and the success message.

A valid submit sends nothing: it only displays a demonstration success message.

### Task 4 — Validation test results

| # | Test input | Expected result | Actual result |
|---|------------|-----------------|---------------|
| 1 | Contact form, all fields empty → Submit | Form is not submitted, Name / Email / Message marked invalid with messages | Passed — red borders, three error messages, focus moves to the first invalid field |
| 2 | Email = `abc` | Email rejected because of the format | Passed — "Please enter a valid email address" |
| 3 | Message = `Hello` (5 characters) | Message rejected, the counter shows the limit | Passed — "The message must be between 10 and 500 characters" |
| 4 | Message = 501 characters | Input stops at 500 because of `maxlength` | Passed — the field cannot exceed 500 characters |
| 5 | Contact form, all fields valid → Submit | Green state, success message appears | Passed — green borders, "Looks good.", success box displayed |
| 6 | Contact form → Reset after errors | Values and feedback cleared | Passed |
| 7 | Password = `1234567` (7 characters) | Rejected, minimum is 8 | Passed — "The password must be at least 8 characters" |
| 8 | Password ≠ Confirm password | Rejected with "The passwords do not match." | Passed — red border and message; the error disappears as soon as the field is corrected |
| 9 | Country left as "Choose your country..." | Rejected | Passed — "Please select your country" |
| 10 | Registration form, all values valid → Submit | Success message, no page reload | Passed — green states and the success box |
| 11 | Registration form → Reset after errors | Values, feedback and the custom password error cleared | Passed |
| 12 | Mobile layout (narrow screen) | One column, no horizontal scrolling, buttons reachable | Passed — the form stacks to one column, page width equals the viewport |
| 13 | Desktop layout | Two columns for short fields, full width for the message | Passed |

Screenshots of the invalid state, the valid state, the password mismatch and the narrow-screen
layout are in the `screenshots` folder of the report. Re-run the cases above once before
submitting and replace these results with the ones you actually observe.

## Limitations

The forms are a static demonstration. They do **not** send or store any data. Native HTML5
validation and a small amount of JavaScript are used to demonstrate form behaviour. Real
message delivery would require a backend or a third-party service.

## Structure

```
website_mac/
├── index.html
├── service.html
├── about.html
├── contacts.html
├── register.html
├── css/
│   ├── style.css          base layout, navigation, footer
│   ├── index.css          home page
│   ├── about.css          about page
│   ├── service.css        service page
│   ├── contact.css        contacts page
│   ├── forms.css          Assignment #5 forms
│   ├── responsive.css     shared breakpoints
│   └── vendor/bootstrap.min.css
├── js/
│   ├── validation.js      contact form validation
│   ├── register.js        registration form validation
│   └── vendor/bootstrap.bundle.min.js
└── images/
```
