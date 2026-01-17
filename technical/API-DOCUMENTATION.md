# 📚 API Documentation (OpenAPI/Swagger Spec)

## Base URL

```
Development:  http://localhost:3300/api
Staging:      https://staging-api.vera.app/api
Production:   https://api.vera.app/api
```

## Authentication

All endpoints require Bearer token (except public endpoints).

```bash
Authorization: Bearer <JWT_TOKEN>

# Token obtained from POST /auth/signup or /auth/login
# Expires in 24 hours
# Refresh with POST /auth/refresh
```

---

## Endpoints Overview

```
AUTH (Public)
├── POST   /auth/signup
├── POST   /auth/login
├── POST   /auth/logout
├── POST   /auth/refresh
└── POST   /auth/reset-password

USERS (Protected)
├── GET    /users/me
├── PUT    /users/me
└── POST   /users/me/export-data

CHILDREN (Protected)
├── GET    /children
├── POST   /children
├── PUT    /children/{id}
├── DELETE /children/{id}
└── GET    /children/{id}/stats

PHOTOS (Protected)
├── POST   /photos/upload
├── POST   /photos/batch-upload
├── GET    /photos/timeline
├── GET    /photos/{id}
├── PUT    /photos/{id}
├── PUT    /photos/{id}/story
├── POST   /photos/{id}/favorite
├── DELETE /photos/{id}
└── GET    /photos/search

TAGS (Protected)
├── GET    /tags
├── POST   /photos/{id}/tags
└── DELETE /photos/{id}/tags/{tagId}

FAMILY SHARING (Protected)
├── POST   /family-shares/invite
├── GET    /family-shares
├── GET    /family-shares/{token}
├── POST   /family-shares/{token}/accept
├── DELETE /family-shares/{id}
└── GET    /family-shares/{id}/photos

ALBUMS (Protected)
├── GET    /albums
├── GET    /albums/{year}
├── PUT    /albums/{year}
├── GET    /albums/{year}/preview
└── POST   /albums/{year}/finalize

SUBSCRIPTIONS (Protected)
├── GET    /subscriptions/current
├── POST   /subscriptions/checkout
├── PUT    /subscriptions/pause
└── POST   /subscriptions/cancel

NOTIFICATIONS (Protected)
├── GET    /notifications
├── PUT    /notifications/{id}/read
└── DELETE /notifications/{id}
```

---

## Detailed Endpoints

### AUTH

#### POST /auth/signup

**Request:**
```json
{
  "email": "user@example.com",
  "password": "SecurePass123!",
  "firstName": "John",
  "lastName": "Doe"
}
```

**Response (201 Created):**
```json
{
  "user": {
    "id": "user-uuid",
    "email": "user@example.com",
    "firstName": "John",
    "lastName": "Doe",
    "createdAt": "2026-01-17T10:00:00Z"
  },
  "token": "eyJhbGciOiJIUzI1NiIs...",
  "refreshToken": "eyJhbGciOiJIUzI1NiIs..."
}
```

**Errors:**
```json
// 400 - Invalid input
{
  "error": "validation_error",
  "details": {
    "email": "Invalid email format",
    "password": "Password must be at least 8 characters"
  }
}

// 409 - Email exists
{
  "error": "email_already_registered",
  "message": "User with this email already exists"
}
```

---

#### POST /auth/login

**Request:**
```json
{
  "email": "user@example.com",
  "password": "SecurePass123!"
}
```

**Response (200 OK):**
```json
{
  "user": {
    "id": "user-uuid",
    "email": "user@example.com",
    "firstName": "John",
    "lastName": "Doe"
  },
  "token": "eyJhbGciOiJIUzI1NiIs...",
  "refreshToken": "eyJhbGciOiJIUzI1NiIs..."
}
```

**Errors:**
```json
// 401 - Invalid credentials
{
  "error": "invalid_credentials",
  "message": "Email or password is incorrect"
}
```

---

#### POST /auth/logout

**Request:**
```json
{
  "refreshToken": "eyJhbGciOiJIUzI1NiIs..."
}
```

**Response (200 OK):**
```json
{
  "message": "Logged out successfully"
}
```

---

### USERS

#### GET /users/me

**Response (200 OK):**
```json
{
  "id": "user-uuid",
  "email": "user@example.com",
  "firstName": "John",
  "lastName": "Doe",
  "profilePhotoUrl": "https://s3.../profile.jpg",
  "subscription": {
    "plan": "premium",
    "status": "active",
    "renewsAt": "2027-01-17T00:00:00Z"
  },
  "children": [
    {
      "id": "child-uuid",
      "name": "Emma",
      "dateOfBirth": "2023-01-17",
      "photoCount": 250
    }
  ],
  "createdAt": "2026-01-17T10:00:00Z"
}
```

---

#### PUT /users/me

**Request:**
```json
{
  "firstName": "John",
  "lastName": "Smith",
  "profilePhotoUrl": "https://s3.../new-profile.jpg"
}
```

**Response (200 OK):**
```json
{
  "id": "user-uuid",
  "email": "user@example.com",
  "firstName": "John",
  "lastName": "Smith",
  "updatedAt": "2026-01-17T11:00:00Z"
}
```

---

#### POST /users/me/export-data

**Description:** GDPR/KVKK data export (JSON format)

**Response (202 Accepted):**
```json
{
  "exportId": "export-uuid",
  "status": "processing",
  "message": "Your data export is being prepared. Check email for download link in 24 hours.",
  "estimatedCompletionTime": "2026-01-18T10:00:00Z"
}
```

---

### PHOTOS

#### POST /photos/upload

**Request (multipart/form-data):**
```
photo: <binary file, max 50MB>
childId: "child-uuid"
metadata: {
  "story": "First upload! 🎉",
  "tags": ["milestones:İlk adım", "location:Park"]
}
```

**Response (200 OK):**
```json
{
  "photo": {
    "id": "photo-uuid",
    "childId": "child-uuid",
    "originalUrl": "https://s3.../original.jpg",
    "thumbnailUrl": "https://cloudfront.../thumb.jpg",
    "webUrl": "https://cloudfront.../web.jpg",
    "exifDate": "2026-01-17T10:00:00Z",
    "calculatedAgeMonths": 36,
    "story": "First upload! 🎉",
    "tags": ["milestones:İlk adım", "location:Park"],
    "uploadedAt": "2026-01-17T11:00:00Z"
  }
}
```

**Errors:**
```json
// 413 - File too large
{
  "error": "file_too_large",
  "message": "File must be smaller than 50MB"
}

// 415 - Unsupported media type
{
  "error": "invalid_file_type",
  "message": "Only JPEG and PNG files are supported"
}
```

---

#### POST /photos/batch-upload

**Request (multipart/form-data):**
```
photos[0]: <binary file>
photos[1]: <binary file>
photos[2]: <binary file>
childId: "child-uuid"
metadata[0]: {"story": "..."}
metadata[1]: {"story": "..."}
metadata[2]: {"story": "..."}
```

**Response (200 OK):**
```json
{
  "photos": [
    {
      "id": "photo-1-uuid",
      "originalUrl": "https://s3.../original1.jpg",
      "uploadedAt": "2026-01-17T11:00:00Z",
      "status": "success"
    },
    {
      "id": "photo-2-uuid",
      "originalUrl": "https://s3.../original2.jpg",
      "uploadedAt": "2026-01-17T11:00:01Z",
      "status": "success"
    }
  ],
  "successCount": 2,
  "failureCount": 1,
  "errors": [
    {
      "fileName": "photo3.jpg",
      "error": "file_too_large",
      "message": "File must be smaller than 50MB"
    }
  ]
}
```

---

#### GET /photos/timeline

**Query Parameters:**
```
childId: "child-uuid" (required)
limit: 50 (optional, default 50)
offset: 0 (optional, default 0)
ageFrom: 0 (optional, months)
ageTo: 60 (optional, months)
```

**Response (200 OK):**
```json
{
  "timeline": [
    {
      "ageMonths": 36,
      "ageDisplay": "3 years",
      "count": 150,
      "photos": [
        {
          "id": "photo-uuid",
          "thumbnailUrl": "https://cloudfront.../thumb.jpg",
          "exifDate": "2026-01-17T10:00:00Z",
          "isFavorite": true
        }
      ]
    },
    {
      "ageMonths": 24,
      "ageDisplay": "2 years",
      "count": 200,
      "photos": [...]
    }
  ],
  "totalCount": 500,
  "hasMore": true
}
```

---

#### GET /photos/{id}

**Response (200 OK):**
```json
{
  "id": "photo-uuid",
  "childId": "child-uuid",
  "originalUrl": "https://s3.../original.jpg",
  "webUrl": "https://cloudfront.../web.jpg",
  "exifDate": "2026-01-17T10:00:00Z",
  "exifCamera": "iPhone 14 Pro",
  "exifGpsLat": 41.0082,
  "exifGpsLng": 28.9784,
  "calculatedAgeMonths": 36,
  "story": "First upload! 🎉",
  "tags": ["milestones:İlk adım"],
  "isFavorite": true,
  "uploadedAt": "2026-01-17T11:00:00Z"
}
```

---

#### PUT /photos/{id}/story

**Request:**
```json
{
  "story": "Updated story about this special moment 💝"
}
```

**Response (200 OK):**
```json
{
  "id": "photo-uuid",
  "story": "Updated story about this special moment 💝",
  "updatedAt": "2026-01-17T12:00:00Z"
}
```

---

#### POST /photos/{id}/favorite

**Request:**
```json
{
  "isFavorite": true
}
```

**Response (200 OK):**
```json
{
  "id": "photo-uuid",
  "isFavorite": true
}
```

---

#### GET /photos/search

**Query Parameters:**
```
childId: "child-uuid"
query: "first step" (optional, full-text search)
tags: "milestones:İlk adım,location:Park" (optional, comma-separated)
dateFrom: "2025-01-17" (optional, ISO date)
dateTo: "2026-01-17" (optional)
ageFrom: 0 (optional)
ageTo: 60 (optional)
limit: 50
offset: 0
```

**Response (200 OK):**
```json
{
  "results": [
    {
      "id": "photo-uuid",
      "thumbnailUrl": "https://cloudfront.../thumb.jpg",
      "story": "First step! 👣",
      "exifDate": "2026-01-17T10:00:00Z",
      "calculatedAgeMonths": 36
    }
  ],
  "totalCount": 25,
  "hasMore": false
}
```

---

### FAMILY SHARING

#### POST /family-shares/invite

**Request:**
```json
{
  "childId": "child-uuid",
  "inviteEmail": "grandma@example.com",
  "canReceiveAlbum": true,
  "expiresIn": 30 (days, optional)
}
```

**Response (201 Created):**
```json
{
  "share": {
    "id": "share-uuid",
    "inviteToken": "token-abc123xyz",
    "inviteEmail": "grandma@example.com",
    "status": "pending",
    "inviteUrl": "https://vera.app/join/token-abc123xyz",
    "expiresAt": "2026-02-17T10:00:00Z",
    "createdAt": "2026-01-17T10:00:00Z"
  }
}
```

---

#### GET /family-shares/{token}/photos

**Description:** Public endpoint for family member to view photos (before accepting invite)

**Response (200 OK):**
```json
{
  "child": {
    "name": "Emma",
    "dateOfBirth": "2023-01-17"
  },
  "photos": [
    {
      "id": "photo-uuid",
      "thumbnailUrl": "https://cloudfront.../thumb.jpg",
      "exifDate": "2026-01-17T10:00:00Z",
      "calculatedAgeMonths": 36,
      "story": "First upload!"
    }
  ]
}
```

---

### ALBUMS

#### GET /albums/{year}

**Response (200 OK):**
```json
{
  "year": 2025,
  "child": {
    "id": "child-uuid",
    "name": "Emma",
    "ageAtYear": 2
  },
  "album": {
    "id": "album-uuid",
    "status": "draft",
    "photoCount": 450,
    "selectedPhotoCount": 450,
    "previewUrl": "https://s3.../preview.pdf",
    "designVariant": "modern",
    "customTitle": "Emma's 2nd Year",
    "createdAt": "2025-01-17T10:00:00Z"
  }
}
```

---

#### PUT /albums/{year}

**Request:**
```json
{
  "designVariant": "modern",
  "customTitle": "Emma's 2nd Year",
  "customMessage": "A year full of memories!",
  "selectedPhotoIds": ["photo-1", "photo-2", "photo-3"]
}
```

**Response (200 OK):**
```json
{
  "id": "album-uuid",
  "year": 2025,
  "status": "updated",
  "photoCount": 300,
  "updatedAt": "2026-01-17T11:00:00Z"
}
```

---

#### GET /albums/{year}/preview

**Description:** Get PDF preview of album

**Response (200 OK - Binary PDF):**
```
Content-Type: application/pdf
Content-Disposition: attachment; filename="Emma-2025.pdf"
[Binary PDF data]
```

---

### SUBSCRIPTIONS

#### GET /subscriptions/current

**Response (200 OK):**
```json
{
  "id": "subscription-uuid",
  "plan": "premium",
  "price": 1999,
  "billingPeriod": "yearly",
  "status": "active",
  "startedAt": "2026-01-17T00:00:00Z",
  "renewsAt": "2027-01-17T00:00:00Z",
  "stripeCustomerId": "cus_xxx",
  "features": {
    "children": 2,
    "familyShares": 5,
    "yearlyAlbum": true,
    "albumPages": 1000
  }
}
```

---

#### POST /subscriptions/checkout

**Request:**
```json
{
  "plan": "premium",
  "billingPeriod": "yearly"
}
```

**Response (200 OK):**
```json
{
  "checkoutUrl": "https://checkout.stripe.com/pay/cs_xxx",
  "sessionId": "cs_xxx"
}
```

---

### NOTIFICATIONS

#### GET /notifications

**Query Parameters:**
```
limit: 20
offset: 0
unreadOnly: false (optional)
```

**Response (200 OK):**
```json
{
  "notifications": [
    {
      "id": "notif-uuid",
      "type": "milestone",
      "title": "Emma took her first step! 👣",
      "body": "Today Emma took her first step. What a milestone!",
      "data": {
        "photoId": "photo-uuid",
        "childId": "child-uuid"
      },
      "sentAt": "2026-01-17T10:00:00Z",
      "readAt": null
    },
    {
      "id": "notif-uuid-2",
      "type": "memory_card",
      "title": "2 years ago today",
      "body": "Emma was only 1 year old! 💝",
      "readAt": "2026-01-17T11:00:00Z"
    }
  ],
  "totalCount": 45,
  "unreadCount": 3
}
```

---

#### PUT /notifications/{id}/read

**Request:**
```json
{}
```

**Response (200 OK):**
```json
{
  "id": "notif-uuid",
  "readAt": "2026-01-17T11:00:00Z"
}
```

---

## Error Responses

### Common Error Codes

```json
// 400 - Bad Request
{
  "error": "validation_error",
  "message": "Invalid input",
  "details": {
    "field": "error message"
  }
}

// 401 - Unauthorized
{
  "error": "unauthorized",
  "message": "Missing or invalid token"
}

// 403 - Forbidden
{
  "error": "forbidden",
  "message": "You don't have permission to access this resource"
}

// 404 - Not Found
{
  "error": "not_found",
  "message": "Resource not found"
}

// 429 - Rate Limited
{
  "error": "rate_limited",
  "message": "Too many requests. Please try again in 60 seconds.",
  "retryAfter": 60
}

// 500 - Server Error
{
  "error": "internal_server_error",
  "message": "Something went wrong. Please try again later."
}
```

---

## Rate Limiting

```
Limits (per user):
├── 100 requests/minute (default)
├── 500 requests/hour
├── 5000 requests/day
└── Photo upload: 10 files/minute, 50 files/hour

Headers:
├── X-RateLimit-Limit: 100
├── X-RateLimit-Remaining: 45
└── X-RateLimit-Reset: 1642425660 (Unix timestamp)
```

---

## Pagination

All list endpoints support pagination:

```
Query parameters:
├── limit: 20 (items per page, max 100)
├── offset: 0 (starting position)

Response:
├── data: [...] (items)
├── totalCount: 500 (total items)
├── hasMore: true (more items exist?)
└── offset: 20 (current offset)
```

---

## Webhooks

```
POST https://your-domain.com/webhooks/vera

Events:
├── photo.uploaded
├── album.ready
├── album.shipped
├── subscription.renewed
├── subscription.cancelled
├── family_share.accepted
└── milestone.detected

Payload:
{
  "id": "webhook-id",
  "event": "photo.uploaded",
  "timestamp": "2026-01-17T10:00:00Z",
  "data": {...}
}
```

---

## Status Codes Summary

| Code | Meaning |
|------|---------|
| 200 | OK |
| 201 | Created |
| 202 | Accepted (async processing) |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 409 | Conflict |
| 413 | Payload Too Large |
| 415 | Unsupported Media Type |
| 429 | Too Many Requests |
| 500 | Internal Server Error |
| 502 | Bad Gateway |
| 503 | Service Unavailable |

---

**Status**: ✅ Ready for backend implementation
