# ■ Design Memo - [SaaS Common Services] SSO List / SAML Create & Update / OIDC Create & Update Screens

### What we want to achieve
Enable administrators to:
- View SSO list.
- Create and update SAML SSO.
- Create and update OIDC SSO.

---

### Work Repository
- **Repository Name:** smo-spa-portal

---

### Tiered Response Plan
- **Plan:** Add Feature
- **Scope:** Create new screens

---

### Access Restrictions
- **View/Edit Roles:** ADMIN

---

### Access Methods
- From the sidebar, click on the **SSO** menu item.
  - This opens the **SSO List Screen**.
  - From there, users can navigate to:
    - **Create SAML Screen**
    - **Update SAML Screen**
    - **Create OIDC Screen**
    - **Update OIDC Screen**

---

### Performance Design
- None specified

---

### URL
| URL | Explanation |
|-----|-------------|
| `/owner/sso` | SSO list screen |
| `/owner/sso/saml/create` | Create new SAML SSO connection |
| `/owner/sso/saml/update` | Update existing SAML SSO connection |
| `/owner/sso/oidc/create` | Create new OIDC SSO connection |
| `/owner/sso/oidc/update` | Update existing OIDC SSO connection |

---



### Management Portal Internationalization
- **Multilingual Support:** Yes
- **Language File:** `src/config/lang/ja.json`

---

### Browser Tab Titles
| Screen | Title |
|--------|-------|
| SSO List | SSO List | Smoker Management Portal |
| SAML Create | Create SAML | Smoker Management Portal |
| SAML Update | Update SAML | Smoker Management Portal |
| OIDC Create | Create OIDC | Smoker Management Portal |
| OIDC Update | Update OIDC | Smoker Management Portal |

---

### Screen Layout
- **SSO List Screen**
  - Table showing existing SSO list
  - Actions: Link, Unlink
  - Buttons: Create SSO (SAML/OIDC)

- **SAML/OIDC Screens**
  - Create SAML/OIDC Screens
  - Update SAML/OIDC

---

### Actions
- **Create SAML/OIDC**
- **Update SAML/OIDC**
- **Link/Unlink (SAML or OIDC) SSO listitems**
- Show update confirmation dialog on Save

---

### New Libraries to Use
- None (as of now)

---

### Design/UI

---

