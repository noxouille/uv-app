# Sprint 1 User Stories

> **What** we're building — requirements and acceptance criteria.  
> **How** to build it → See `tasks/` folder.

---

## US-001: Create User Profile

**As a** user  
**I want to** create a personalized profile with my household details and preferences  
**So that** the meal recommendations match my actual needs and constraints

### Acceptance Criteria

1. **Household Composition**
   - [ ] User can specify number of adults (≥1)
   - [ ] User can specify number of children (≥0)
   - [ ] User can optionally specify children's ages

2. **Dietary Preferences**
   - [ ] User can select diet type (omnivore, vegetarian, vegan, pescatarian, flexitarian)
   - [ ] User can optionally select preferred cuisines

3. **Dietary Restrictions**
   - [ ] User can select allergies from a list
   - [ ] User can specify foods to avoid

4. **Budget Constraints**
   - [ ] User can set weekly food budget in CAD
   - [ ] System validates budget is positive

5. **Time Constraints**
   - [ ] User can select typical cooking time (quick/medium/elaborate)
   - [ ] User can select days available for cooking

6. **Cooking Mode**
   - [ ] User can choose between daily cooking or batch cooking

7. **Data Persistence**
   - [ ] Profile is saved and retrievable
   - [ ] User receives confirmation

### Business Rules

- At least 1 adult required
- Budget must be positive if provided
- Allergies affect recipe recommendations

### Related Tasks

- [task-001-database-setup.md](tasks/task-001-database-setup.md)
- [task-002-user-model.md](tasks/task-002-user-model.md)
- [task-003-profile-api.md](tasks/task-003-profile-api.md)
- [task-004-profile-form-ui.md](tasks/task-004-profile-form-ui.md)

---

## US-002: Set Geographic Zone

**As a** user  
**I want to** specify my location and maximum travel distance for shopping  
**So that** promotions and recommendations are actually accessible to me

### Acceptance Criteria

1. **Location Input**
   - [ ] User can enter Canadian postal code (format: A1A 1A1)
   - [ ] System validates postal code format
   - [ ] System geocodes postal code to coordinates

2. **Travel Distance**
   - [ ] User can select max travel distance (preset options: 1, 5, 10, 15, 25 km)
   - [ ] Default is 10 km

3. **Zone Validation**
   - [ ] System checks if location is in serviceable area
   - [ ] If not serviceable, show friendly message with waitlist option
   - [ ] MVP focus: Quebec major cities (Montreal, Quebec City, Laval, Gatineau)

4. **Store Preferences** (Optional for MVP)
   - [ ] User can select preferred store chains

5. **Data Persistence**
   - [ ] Location saved with profile
   - [ ] Can be updated later

### Business Rules

- Postal code must be valid Canadian format
- Service limited to defined geographic zones for MVP
- Geocoding happens asynchronously

### Related Tasks

- [task-005-location-model.md](tasks/task-005-location-model.md)
- [task-006-geocoding-service.md](tasks/task-006-geocoding-service.md)
- [task-007-location-ui.md](tasks/task-007-location-ui.md)

---

## US-011: User Registration/Login (Stretch)

**As a** user  
**I want to** create an account and log in  
**So that** my profile is accessible across devices

### Acceptance Criteria

1. **Registration**
   - [ ] User can register with email/password
   - [ ] Email format is validated
   - [ ] Password must be at least 8 characters
   - [ ] System checks email uniqueness

2. **Login**
   - [ ] User can log in with email/password
   - [ ] Session/token is created

3. **Security**
   - [ ] Passwords are hashed
   - [ ] HTTPS required

### Notes

- Can be deferred to Sprint 2
- MVP can work with anonymous/device-based profiles

### Related Tasks

- [task-008-auth-system.md](tasks/task-008-auth-system.md)

---

## Story Dependencies

```
US-001: Create Profile
    │
    ├── enables: US-002
    └── enables: Future stories (menu, shopping list)

US-002: Set Geographic Zone
    │
    └── depends on: US-001
    └── enables: US-005 (promotions)
```
