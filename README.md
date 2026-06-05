# Tradey API 🎮

> A RESTful API for a peer-to-peer video game trading platform — built with Flask, SQLAlchemy, and JWT authentication.

Tradey lets gamers list used games, send trade requests, respond to them, and rate completed exchanges — reducing game wastage through a safe, structured trading environment.

---

## Tech Stack

Python · Flask · Flask-Smorest · SQLAlchemy · Flask-JWT-Extended · Marshmallow · SQLite · smtplib · OpenAPI/Swagger

---

## Getting Started

```bash
git clone https://github.com/your-username/tradey-api.git
cd tradey-api
python -m venv venv && source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt
flask run
```

API: `http://localhost:5000` — Swagger UI: `http://localhost:5000/swagger-ui`

---

## Environment Variables

Store in `.flaskenv`:

| Variable | Description |
|---|---|
| `JWT_SECRET_KEY` | Secret key for signing JWT tokens |
| `DATABASE_URL` | DB URI (defaults to `sqlite:///data.db`) |
| `SENDER_EMAIL` | Email used to send verification codes |
| `APP_PASSWORD` | App password for the sender email |

---

## API Testing

Test via **Swagger UI** at `/swagger-ui` (no setup needed), or use [Insomnia](https://insomnia.rest/download) / [Postman](https://www.postman.com/downloads/).

For protected endpoints, add the JWT token from `/login` to every request:
```
Authorization: Bearer <access_token>
```

---

## Authentication Flow

```
1. POST /users   → Register → verification code sent to email
2. POST /login   → username + password + verification_code → returns access_token
3. Use token     → Authorization: Bearer <access_token>
```

---

## API Endpoints

### Users
| Method | Endpoint | Auth |
|---|---|---|
| POST | `/users` | No |
| POST | `/login` | No |
| GET | `/users` | No |
| GET / PUT / DELETE | `/users/<username>` | ✅ JWT |

### Games
| Method | Endpoint | Auth |
|---|---|---|
| POST | `/games` | ✅ JWT |
| GET | `/games` | No |
| GET | `/games/<username>` | ✅ JWT |
| GET | `/game/<game_id>` | No |
| DELETE | `/game/<username>/<game_id>` | ✅ JWT |

### Trade Requests
| Method | Endpoint | Auth |
|---|---|---|
| POST | `/traderequests` | ✅ JWT |
| GET | `/traderequests` | No |
| GET | `/traderequests/<username>/sent` | ✅ JWT |
| GET | `/traderequests/<username>/received` | ✅ JWT |
| GET | `/traderequests/<username>/received/<request_id>` | ✅ JWT |
| DELETE | `/traderequests/<username>/<request_id>` | ✅ JWT |

### Trade Responses
| Method | Endpoint | Auth |
|---|---|---|
| POST | `/traderesponses` | ✅ JWT |
| GET | `/traderesponses` | No |
| GET | `/traderesponses/<username>/sent` | ✅ JWT |
| GET | `/traderesponses/<username>/received` | ✅ JWT |
| GET | `/traderesponses/<username>/received/<response_id>` | ✅ JWT |

### Ratings
| Method | Endpoint | Auth |
|---|---|---|
| POST | `/ratings` | ✅ JWT |
| GET | `/ratings` | No |
| GET | `/ratings/<rating_id>` | No |