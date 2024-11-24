# Role-Based Access Control (RBAC)

[![NPM version](https://img.shields.io/npm/v/rbac.svg?style=flat-square)](https://www.npmjs.com/package/rbac)  
[![Build Status](https://img.shields.io/travis/seeden/rbac/master.svg?style=flat-square)](https://travis-ci.org/seeden/rbac)  
[![Test Coverage](https://img.shields.io/coveralls/seeden/rbac/master.svg?style=flat-square)](https://coveralls.io/r/seeden/rbac?branch=master)  

**RBAC** is a hierarchical **role-based access control library** for Node.js, created and maintained by **[Vinay-014](https://github.com/Vinay-014)**. This library allows seamless management of user roles and permissions in applications requiring complex access hierarchies.

---

## 🚀 Key Features

- **Hierarchical Role Management**: Define and manage roles and permissions effortlessly.
- **Multiple Storage Support**: Works with in-memory, Mongoose, or DynamoDB (via [dynamoose](https://github.com/automategreen/dynamoose)).
- **Asynchronous API**: Ensures smooth integration with modern JavaScript frameworks.
- **Express.js Ready**: Built-in support for middleware integration.

---

## 📦 Installation

To install RBAC, use npm:

```bash
npm install rbac
```

---

## 💡 Quick Start Guide

### Basic Configuration

```javascript
import { RBAC } from 'rbac'; // For ES5: const RBAC = require('rbac').default;

const rbac = new RBAC({
  roles: ['superadmin', 'admin', 'user', 'guest'],
  permissions: {
    user: ['create', 'delete'],
    password: ['change', 'forgot'],
    article: ['create'],
    rbac: ['update'],
  },
  grants: {
    guest: ['create_user', 'forgot_password'],
    user: ['change_password'],
    admin: ['user', 'delete_user', 'update_rbac'],
    superadmin: ['admin'],
  },
});

await rbac.init();
```

---

### Express.js Integration

```javascript
import express from 'express';
import { RBAC } from 'rbac';
import secure from 'rbac/controllers/express';

const app = express();
const rbac = new RBAC({ roles: ['admin', 'user'] });

await rbac.init();

app.use('/admin', secure.hasRole(rbac, 'admin'), (req, res) => {
  res.send('Welcome Admin!');
});
```

---

### Checking Permissions

```javascript
const can = await rbac.can('admin', 'create', 'article');
if (can) {
  console.log('Admin can create articles');
}
```

---

## 📚 Documentation

For detailed API documentation, [click here](http://seeden.github.io/rbac/RBAC.html).

---

## 🛠️ Development

### Building the Library

```bash
npm run build
```

### Running Tests

```bash
npm run test
```

### Generating Documentation

```bash
npm run doc
```

---

## 🙌 Credits

This library is maintained by **[Vinay-014](https://github.com/Vinay-014)**.

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).  
