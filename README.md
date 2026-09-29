# Appointments Made Easy

A scheduling platform that removes the back-and-forth of booking. Two roles — **students** who book
and **facilities** that get booked — with authentication on both sides and **automated email
notifications** so neither party ever has to chase the other.

## Features

### Two-sided booking
- **Student side** — register, sign in, browse facilities, view booking details, and manage their own
  bookings
- **Facility side** — register, sign in, manage the facility profile, and review incoming bookings

### Authentication
- `passport-local-mongoose` for sign-in, with **bcrypt** password hashing
- `express-session` for session handling
- Role-separated views so students and facilities see different dashboards

### Email automation
`nodemailer` + `mailgen` generate and send styled notification emails, so a booking, reschedule or
cancellation reaches the right inbox automatically.

### Data security
Sensitive fields are encrypted at rest with `mongoose-encryption`, so the database never holds
plaintext where it shouldn't.

## Tech stack

| Concern | Technology |
|---|---|
| Runtime | Node.js ≥ 16 |
| Server | Express 4 (ES modules) |
| Views | EJS |
| Database | MongoDB via Mongoose 6 |
| Auth | Passport (local strategy), bcrypt, express-session |
| Email | Nodemailer + Mailgen |
| Encryption | mongoose-encryption |
| Config | dotenv |

## Getting started

```bash
cd apmtdup3
npm install
```

```bash
# .env  — these are the exact names index.js reads
SECRET=<session secret>
CONNECTIONSTRING=mongodb://127.0.0.1:27017/appointments
EMAIL=<smtp account used to send>
PASSWORD=<smtp account password>
API_KEY=<optional, currently unused — referenced but commented out>
```

There is no `.env.example` in the repo, so the names above are taken directly from `index.js`.
The SMTP host/port are configured in the `nodemailer` transport block rather than read from the
environment.

Make sure MongoDB is running locally, or point `CONNECTIONSTRING` at a hosted instance.

```bash
npm start        # node index.js
```

Then open **http://localhost:3000**.

> Email sending needs valid SMTP credentials. Without them, bookings still work and notifications are
> simply skipped.

## Views

**Student**

| View | Purpose |
|---|---|
| `sthome.ejs` | Student home |
| `slogin.ejs` / `stregister.ejs` | Auth |
| `apmt.ejs` | Make an appointment |
| `mybookings.ejs` | The student's own bookings |

**Facility**

| View | Purpose |
|---|---|
| `fdashboard.ejs` | Facility dashboard |
| `flogin.ejs` / `facregister.ejs` | Auth |
| `fgeneral.ejs` | Facility profile |
| `facdet.ejs` | Facility detail |
| `facbookings.ejs` | Incoming bookings |
| `favb.ejs` | Availability / booking management |

Plus `home.ejs` and `dshbd.ejs` at the top level.

## Project layout

```
apmtdup3/
├── index.js           Express app entry point
├── views/             EJS templates (student + facility)
├── public/            static assets (css, images)
└── package.json
```

## License

ISC
