![Stack Logo](/.github/assets/logo.png)

<h3 align="center">
  <a href="https://docs.stack-auth.com">📘 Docs</a>
  | <a href="https://stack-auth.com/">☁️ Hosted Version</a>
  | <a href="https://demo.stack-auth.com/">✨ Demo</a>
  | <a href="https://discord.stack-auth.com">🎮 Discord</a>
</h4>

# Stack Auth: Open-source Clerk/Auth0 alternative

Stack Auth is a managed user authentication solution. It is developer-friendly and fully open-source (licensed under MIT and AGPL).

Stack gets you started in just five minutes, after which you'll be ready to use all of its features as you grow your project. Our managed service is completely optional and you can export your user data and self-host, for free, at any time.

We support Next.js frontends, along with any backend that can use our [REST API](https://docs.stack-auth.com/rest-api/auth). Check out our [setup guide](https://docs.stack-auth.com/getting-started/setup) to get started.

<div align="center">
<img alt="Stack Setup" src=".github/assets/create-project.gif" width="400" />
</div>

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## ✨ Features

To get notified first when we add new features, please subscribe to [our newsletter].

| | |
|-|:-:|
| <h3>`<SignIn/>` and `<SignUp/>`</h3> Authentication components that support OAuth, password credentials, and magic links, with shared development keys to make setup faster. All components support dark/light modes. | <img alt="Sign-in component" src=".github/assets/dark-light-mode.png" width="250px"> |
| <h3>Idiomatic Next.js APIs</h3> We build on server components, React hooks, and route handlers. | ![Dark/light mode](.github/assets/components.png) |
| <h3>User dashboard</h3> Dashboard to filter, analyze, and edit users. Replaces the first internal tool you would have to build. | ![User dashboard](.github/assets/dashboard.png) |
| <h3>Account settings</h3> Lets users update their profile, verify their e-mail, or change their password. No setup required. | <img alt="Account settings component" src=".github/assets/account-settings.png" width="300px"> |
| <h3>Multi-tenancy & teams</h3> Manage B2B customers with an organization structure that makes sense and scales to millions. | <img alt="Selected team switcher component" src=".github/assets/team-switcher.png" width="400px"> |
| <h3>Role-based access control</h3> Define an arbitrary permission graph and assign it to users. Organizations can create org-specific roles. | <img alt="RBAC" src=".github/assets/permissions.png"  width="400px"> |
| <h3>OAuth Connections</h3>Beyond login, Stack can also manage access tokens for third-party APIs, such as Outlook and Google Calendar. It handles refreshing tokens and controlling scope, making access tokens accessible via a single function call. | <img alt="OAuth tokens" src=".github/assets/connected-accounts.png"  width="250px"> |
| <h3>Passkeys</h3> Support for passwordless authentication using passkeys, allowing users to sign in securely with biometrics or security keys across all their devices. | <img alt="OAuth tokens" src=".github/assets/passkeys.png"  width="400px"> |
| <h3>Webhooks</h3> Get notified when users use your product, built on Svix. | <img alt="Webhooks" src=".github/assets/stack-webhooks.png"  width="300px"> |
| <h3>Automatic emails</h3> Send customizable emails on triggers such as sign-up, password reset, and email verification, editable with a WYSIWYG editor. | <img alt="Email templates" src=".github/assets/email-editor.png"  width="400px"> |
| <h3>User session & JWT handling</h3> Stack manages refresh and access tokens, JWTs, and cookies, resulting in the best performance at no implementation cost. | <img alt="User button" src=".github/assets/user-button.png"  width="400px"> |
| <h3>M2M authentication</h3> Use short-lived access tokens to authenticate your machines to other machines. | <img src=".github/assets/m2m-auth.png" alt="M2M authentication"  width="400px"> |


## 📦 Installation & Setup

1. Run Stack’s installation wizard with the following command:
    ```bash
    npx @stackframe/init-stack@latest
    ```
2. Then, create an account on the Stack Auth dashboard, create a new project with an API key, and copy its environment variables into the .env.local file of your Next.js project:
    ```
    NEXT_PUBLIC_STACK_PROJECT_ID=<your-project-id>
    NEXT_PUBLIC_STACK_PUBLISHABLE_CLIENT_KEY=<your-publishable-client-key>
    STACK_SECRET_SERVER_KEY=<your-secret-server-key>
    ```
3. That's it! You can run your app with `npm run dev` and go to [http://localhost:3000/handler/signup](http://localhost:3000/handler/signup) to see the sign-up page. You can also check out the account settings page at [http://localhost:3000/handler/account-settings](http://localhost:3000/handler/account-settings).

Check out the [documentation](https://docs.stack-auth.com/getting-started/setup) for a more detailed guide.

## 🏗 Development & Contribution

This is for you if you want to contribute to the Stack project or run the Stack dashboard locally.

**Important**: Please read the [contribution guidelines](CONTRIBUTING.md) carefully and join [our Discord](https://discord.stack-auth.com) if you'd like to help.

### Requirements

- Node v20
- pnpm v9
- Docker

### Setup

Pre-populated .env files for the setup below are available and used by default in `.env.development` in each of the packages. (Note: If you're creating a production build (eg. with `pnpm run build`), you must supply the environment variables manually.)

In a new terminal:

```sh
pnpm install

# Run build to build everything once
pnpm run build:dev

# reset & start the dependencies (DB, Inbucket, etc.) as Docker containers, seeding the DB with the Prisma schema
pnpm run start-deps
# pnpm run restart-deps
# pnpm run stop-deps

# Start the dev server
pnpm run dev

# In a different terminal, run tests in watch mode
pnpm run test
```

You can now open the dashboard at [http://localhost:8101](http://localhost:8101), API on port 8102, demo on port 8103, docs on port 8104, Inbucket (e-mails) on port 8105, and Prisma Studio on port 8106. See the section below on more information on the ports of the running services.

Your IDE may show an error on all `@stackframe/XYZ` imports. To fix this, simply restart the TypeScript language server; for example, in VSCode you can open the command palette (Ctrl+Shift+P) and run `Developer: Reload Window` or `TypeScript: Restart TS server`.

You can also open Prisma Studio to see the database interface and edit data directly:

```sh
pnpm run prisma studio
```

### Development environment port mapping

`8101`: Dashboard `apps/dashboard` (equivalent to https://app.stack-auth.com)  
`8102`: Backend `apps/backend` (equivalent to https://api.stack-auth.com)  
`8103`: Demo app `examples/demo` (equivalent to https://demo.stack-auth.com)  
`8104`: Docs `docs` (equivalent to https://docs.stack-auth.com)  
`8105`: Inbucket (e-mails)  
`8106`: Prisma Studio  
`8107`: Jaeger UI/OpenTelemetry (for performance tracing)  
`8108`: `examples/docs-examples`  
`8109`: `examples/partial-prerendering`  
`8110`: `examples/cjs-test`  
`8111`: `examples/e-commerce`  
`8112`: `examples/middleware`  
`8113`: Svix server (for webhooks)  
`8114`: OAuth mock server  
`8115`: `examples/supabase`  


### Database migrations

If you make changes to the Prisma schema, you need to run the following command to create a migration:

```sh
pnpm run prisma migrate dev
```

### Chat with the codebase

Storia trained an [AI on our codebase](https://sage.storia.ai/stack-auth) that can answer questions about using and contributing to Stack.

Thanks to [CodeViz](https://www.codeviz.ai) for generating the diagram!