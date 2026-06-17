# Authgate Production Service Roadmap

## 1. Authentication and authorization fundamentals

### 001. Separate authentication and authorization

Record the differences between establishing a user's identity and checking their right to perform a specific action.

### 002. Research the identity lifecycle

Examine identity registration, verification, activation, suspension, recovery, deactivation, and deletion.

### 003. Research the credential lifecycle

Examine credential creation, rotation, compromise, revocation, and expiration.

### 004. Research session-based authentication

Define the model of server-side sessions, session identifiers, cookies, and session storage.

### 005. Research token-based authentication

Examine access tokens, refresh tokens, bearer semantics, and the limitations of stateless authentication.

### 006. Compare opaque and self-contained tokens

Record the differences in introspection, revocation, latency, payload exposure, and key management.

### 007. Research authentication assurance levels

Define trust levels for password, MFA, WebAuthn, and step-up authentication.

### 008. Research RBAC

Examine users, roles, permissions, assignments, and role hierarchy.

### 009. Research ABAC

Examine subject, resource, action, environment attributes, and policy evaluation.

### 010. Research ACL

Define use cases for resource-level access control lists.

### 011. Research ReBAC

Examine access based on relationships between user, team, organization, and resource.

### 012. Research policy-based authorization

Define the structure of policies, decisions, obligations, and deny reasons.

### 013. Research OAuth 2.0

Examine resource owner, client, authorization server, resource server, and authorization grants.

### 014. Research OpenID Connect

Define the purpose of ID Token, UserInfo, and identity claims on top of OAuth 2.0.

### 015. Research Zero Trust

Record the principle of continuous verification of identity, device, context, and requested action.

### 016. Research defense in depth

Define protection layers at the transport, application, data, and operational layers.

### 017. Research least privilege

Prohibit granting credentials and permissions broader than the required scope.

### 018. Research the confused deputy problem

Examine situations in which a trusted backend performs an action on behalf of an insufficiently authorized caller.

### 019. Define trust boundaries

Record the boundaries between browser, API, auth service, resource services, database, and external identity providers.

### 020. Record security invariants

Document mandatory rules for credential storage, session validation, authorization, and audit.

## 2. Repository structure and infrastructure

### 021. Create a monorepo

Configure a workspace for Auth API, background workers, administration CLI, and shared libraries.

### 022. Create NestJS Auth API

Implement the main HTTP application for authentication, sessions, API keys, and authorization.

### 023. Create a background worker

Separate a process for email, cleanup, audit export, and security notifications.

### 024. Create an administration CLI

Add commands for managing users, sessions, keys, roles, and security incidents.

### 025. Define shared libraries

Separate domain, application, contracts, database, crypto, observability, and testing packages.

### 026. Configure TypeScript strict mode

Enable strict type checking, nullability, and unsafe operations checks.

### 027. Configure project references

Separate the build of applications and libraries with controlled dependencies.

### 028. Configure path aliases

Create stable aliases for domain, application, adapters, and shared packages.

### 029. Configure ESLint

Add rules for Promise handling, security-sensitive code, and prohibited imports.

### 030. Configure Prettier

Ensure a consistent format for TypeScript, JSON, YAML, and Markdown.

### 031. Configure environment validation

Validate PostgreSQL, Redis, RabbitMQ, signing keys, cookie settings, and email provider configuration.

### 032. Create a Docker Compose environment

Add PostgreSQL, Redis, RabbitMQ, Mailpit, and an observability stack.

### 033. Configure PostgreSQL migrations

Create a reproducible migration workflow for development, test, and production.

### 034. Create development seeds

Prepare users, roles, permissions, sessions, clients, and API keys.

### 035. Configure application bootstrap

Connect validation, error handling, security headers, logging, and tracing.

### 036. Implement a liveness endpoint

Check process operability without accessing external dependencies.

### 037. Implement a readiness endpoint

Check PostgreSQL, Redis, broker, and required cryptographic materials.

### 038. Implement graceful shutdown

Correctly terminate HTTP requests, workers, consumers, and database connections.

### 039. Configure configuration profiles

Separate development, test, staging, and production settings.

### 040. Create a local quick-start script

Automate infrastructure startup, migrations, seeds, and applications.

## 3. Architecture and domain boundaries

### 041. Define Authgate modules

Separate Identity, Credentials, Sessions, Tokens, API Keys, Authorization, OAuth, and Audit.

### 042. Define bounded contexts

Record the responsibility and data ownership of each module.

### 043. Design Hexagonal Architecture

Separate domain, application, ports, adapters, delivery, and infrastructure layers.

### 044. Define aggregate boundaries

Separate User, Credential, Session, APIKey, OAuthClient, Role, and Policy aggregates.

### 045. Create the domain layer

Place entities, value objects, domain services, policies, and events without framework dependencies.

### 046. Create the application layer

Place use cases, commands, queries, ports, and transaction orchestration.

### 047. Create the infrastructure layer

Implement PostgreSQL, Redis, crypto, messaging, and external identity adapters.

### 048. Create the delivery layer

Implement HTTP controllers, CLI commands, and broker consumers.

### 049. Define repository ports

Isolate the application layer from ORM and database implementation.

### 050. Define TransactionPort

Allow use cases to perform atomic operations without depending on ORM.

### 051. Define PasswordHasherPort

Isolate the password hashing algorithm from domain logic.

### 052. Define TokenSignerPort

Isolate JWT and opaque token generation from use cases.

### 053. Define SessionStorePort

Support PostgreSQL, Redis, or hybrid session storage.

### 054. Define EmailSenderPort

Separate verification and reset notifications from the email provider.

### 055. Define ClockPort

Enable deterministic testing of expiration and rotation.

### 056. Define RandomGeneratorPort

Use cryptographically secure identifiers and secrets.

### 057. Use explicit DI tokens

Do not rely on runtime TypeScript interfaces for dependency injection.

### 058. Prohibit infrastructure imports in domain

Add automatic architecture checks.

### 059. Prohibit deep imports between modules

Export only public contracts and application ports.

### 060. Document dependency direction

Record allowed dependencies between layers and modules.

## 4. Identity model and user lifecycle

### 061. Design the User entity

Add id, status, primaryEmail, timestamps, and security metadata.

### 062. Create the UserId value object

Prevent accidental mixing of user identifiers with other IDs.

### 063. Create the Email value object

Add normalization, validation, and case-insensitive comparison.

### 064. Define the email uniqueness policy

Record global uniqueness and address reuse rules.

### 065. Separate User and UserProfile

Separate authentication identity from display name and application-specific data.

### 066. Implement the User status machine

Support pending, active, locked, suspended, deactivated, and deleted states.

### 067. Implement user registration

Create a pending identity with an unverified email.

### 068. Implement registration idempotency

Do not create duplicate users on repeated request.

### 069. Implement account activation

Activate identity after completing required verification steps.

### 070. Implement account suspension

Block authentication without deleting credentials and audit history.

### 071. Implement account reactivation

Restore access after an administrative decision.

### 072. Implement account lock

Temporarily block authentication after a security event.

### 073. Implement account unlock

Support automatic and administrative unlock.

### 074. Implement account deactivation

Revoke the user's sessions, refresh tokens, and API keys.

### 075. Implement an account deletion request

Create a managed workflow with a retention period.

### 076. Implement soft deletion

Hide identity from regular queries without physically deleting security records.

### 077. Implement account anonymization

Remove optional PII without damaging audit and authorization history.

### 078. Implement an identity merge policy

Define safe merging of duplicate identities.

### 079. Create user lifecycle events

Publish UserRegistered, UserActivated, UserSuspended, and UserDeactivated.

### 080. Test user lifecycle invariants

Check allowed transitions and mandatory credential revocation.

## 5. Password credentials

### 081. Design the PasswordCredential entity

Store userId, passwordHash, algorithm, parameters, and timestamps.

### 082. Use Argon2id

Configure memory cost, time cost, and parallelism for the production environment.

### 083. Research bcrypt and scrypt

Compare algorithm properties and record the reasons for choosing Argon2id.

### 084. Create a password hashing benchmark

Select hashing parameters according to security and latency targets.

### 085. Implement per-password salt

Use a unique cryptographic salt for each credential.

### 086. Implement pepper

Add an application-level secret separately from the database.

### 087. Implement password verification

Compare hashes through a secure library implementation.

### 088. Implement hash parameter upgrade

Rehash the password after successful login when parameters are outdated.

### 089. Implement a password policy

Check minimum length and prohibited credential categories.

### 090. Do not restrict password composition with artificial rules

Do not require mandatory characters that reduce real entropy through predictable patterns.

### 091. Check compromised passwords

Integrate a local or external breach dataset.

### 092. Implement password history

Prohibit reuse of recent credentials when required by policy.

### 093. Implement password change

Require the current password or step-up authentication.

### 094. Implement forced password change

Support an administrative requirement without storing a temporary plaintext password.

### 095. Invalidate sessions after password change

Terminate selected or all sessions according to security policy.

### 096. Implement credential version

Increment the version on password change for token invalidation.

### 097. Implement a password expiration policy

Support configurable expiration only for environments where it is required.

### 098. Protect password endpoints

Add rate limiting, audit, and sensitive-field redaction.

### 099. Implement a constant-shape login response

Do not reveal user existence through differing messages.

### 100. Test password credential security

Check hashing, migration, reuse, timing, and invalidation scenarios.

## 6. Email verification and password reset

### 101. Design the VerificationToken entity

Store token hash, purpose, userId, expiresAt, usedAt, and metadata.

### 102. Generate cryptographically secure tokens

Use sufficient entropy and URL-safe encoding.

### 103. Store verification tokens as hashes

Do not save the raw token in the database.

### 104. Implement an email verification request

Create a one-time token and send a verification link.

### 105. Implement email verification completion

Check hash, purpose, expiration, and usage state.

### 106. Implement verification token rotation

Invalidate the previous active token on resend.

### 107. Implement verification resend

Add cooldown and rate limiting.

### 108. Implement verification expiration

Reject expired tokens with a safe error response.

### 109. Implement an email change request

Require confirmation of the new email and step-up authentication.

### 110. Implement email change completion

Atomically update primaryEmail and invalidation metadata.

### 111. Design PasswordResetRequest

Store token hash, userId, expiresAt, usedAt, and request context.

### 112. Implement a password reset request

Return the same response for an existing and unknown email.

### 113. Implement password reset completion

Check the token and update the credential in one transaction.

### 114. Invalidate the reset token after use

Prohibit replay of a successful reset request.

### 115. Invalidate old reset tokens

Revoke all incomplete tokens after a successful password change.

### 116. Revoke sessions after password reset

Terminate existing sessions and refresh token families.

### 117. Send a security notification

Notify the user about password change and reset completion.

### 118. Implement reset abuse protection

Limit request frequency by email, IP, and device fingerprint.

### 119. Add audit for verification and reset

Record request, success, failure, and token replay.

### 120. Test recovery flows

Check expiration, duplicate requests, replay, and concurrent completion.

## 7. Sessions and cookies

### 121. Design the Session entity

Store sessionId, userId, status, createdAt, lastSeenAt, and expiresAt.

### 122. Store session identifiers as hashes

Do not save the raw session cookie in the database.

### 123. Generate secure session identifiers

Use cryptographically secure random values.

### 124. Implement session creation

Create a session only after successful authentication.

### 125. Implement session validation

Check status, expiration, user status, and credential version.

### 126. Implement absolute expiration

Limit the maximum session lifetime.

### 127. Implement idle expiration

Terminate the session after a period of inactivity.

### 128. Implement sliding expiration

Extend the session within the absolute lifetime.

### 129. Implement last-seen throttling

Do not update the session record on every request.

### 130. Implement session rotation

Change the session identifier after login and privilege elevation.

### 131. Protect against session fixation

Never preserve the pre-authentication session identifier after login.

### 132. Configure secure cookies

Use HttpOnly, Secure, SameSite, and a restricted Path.

### 133. Define the cookie domain policy

Do not expand cookie scope to unnecessary subdomains.

### 134. Implement CSRF protection

Use a synchronizer token or double-submit pattern for cookie auth.

### 135. Implement session revocation

Allow termination of one selected session.

### 136. Implement revoke-all sessions

Terminate all user sessions except the current one or including it.

### 137. Implement a device session list

Show device metadata, location approximation, and last activity.

### 138. Implement suspicious session detection

Record abrupt changes in device, ASN, or geography.

### 139. Implement Redis session cache

Accelerate validation without losing authoritative PostgreSQL state.

### 140. Test the session lifecycle

Check rotation, expiration, revocation, CSRF, and concurrent requests.

## 8. Access tokens and refresh tokens

### 141. Design AccessToken claims

Add subject, issuer, audience, issuedAt, expiresAt, sessionId, and scopes.

### 142. Minimize JWT payload

Do not include PII and mutable authorization data unless necessary.

### 143. Implement asymmetric token signing

Use RSA or ECDSA keys to separate signing and verification.

### 144. Implement key identifiers

Add `kid` for verification key selection.

### 145. Create a JWKS endpoint

Publish active public keys for resource services.

### 146. Implement signing key rotation

Support current and previous verification keys simultaneously.

### 147. Check issuer and audience

Do not accept a token issued for another service or environment.

### 148. Check token lifetime

Validate exp, nbf, and allowed clock skew.

### 149. Check the signature algorithm

Prohibit algorithm confusion and unsupported algorithms.

### 150. Design the RefreshToken entity

Store token hash, familyId, sessionId, status, and expiration.

### 151. Implement refresh token rotation

Issue a new token on every successful refresh.

### 152. Implement refresh token reuse detection

Detect repeated use of an already rotated token.

### 153. Revoke the refresh token family

Terminate the entire chain when reuse is detected.

### 154. Bind the refresh token to the session

Do not allow refresh after session revocation or expiration.

### 155. Implement refresh token absolute expiration

Limit the maximum lifetime regardless of rotation.

### 156. Implement refresh token idle expiration

Terminate unused token families.

### 157. Implement opaque refresh tokens

Do not expose internal claims in a client-visible token.

### 158. Implement token introspection

Provide a protected endpoint for checking an opaque or revocable token.

### 159. Implement a token revocation endpoint

Allow the client to revoke a refresh or access token reference.

### 160. Test the token lifecycle

Check rotation, reuse, key rollover, audience, and revocation.

## 9. MFA, step-up authentication, and passkeys

### 161. Design AuthenticationFactor

Support password, TOTP, WebAuthn, and recovery code types.

### 162. Implement MFA enrollment state

Separate pending, active, suspended, and revoked factor states.

### 163. Implement TOTP enrollment

Generate a secret, provisioning URI, and initial verification challenge.

### 164. Store TOTP secrets securely

Encrypt secrets at rest and restrict access by application role.

### 165. Implement TOTP verification

Check the allowed time window and prevent replay of the same code.

### 166. Implement TOTP removal

Require step-up authentication or a recovery procedure.

### 167. Implement recovery codes

Generate one-time codes and store only hashes.

### 168. Implement recovery code consumption

Atomically mark a code as used.

### 169. Implement recovery code regeneration

Invalidate the previous set after identity confirmation.

### 170. Research WebAuthn

Examine authenticator, credential, challenge, origin, and relying party.

### 171. Implement WebAuthn registration

Check challenge, origin, RP ID, and attestation result.

### 172. Implement WebAuthn authentication

Check assertion, signature counter, and user presence.

### 173. Support discoverable credentials

Implement passkey login without prior username entry.

### 174. Handle cloned authenticator signals

Respond to an incorrect change in the signature counter.

### 175. Implement the MFA challenge entity

Store purpose, factor, expiration, and attempt limits.

### 176. Implement step-up authentication

Increase assurance level for critical operations.

### 177. Implement remembered device

Create a restricted trusted-device credential with expiration.

### 178. Implement MFA policy

Require MFA by role, tenant, risk level, or operation.

### 179. Implement MFA recovery

Create a protected process without bypassing existing factors.

### 180. Test MFA flows

Check enrollment, replay, recovery, step-up, and factor revocation.

## 10. API keys and machine credentials

### 181. Design the APIKey entity

Store owner, prefix, hash, scopes, status, and expiration.

### 182. Generate an API key secret

Use a cryptographically secure random value of sufficient length.

### 183. Store API keys as hashes

Show the raw secret only once after creation.

### 184. Implement an API key prefix

Use a prefix to find the key record and identify the environment.

### 185. Implement API key creation

Check owner authorization, scopes, and expiration policy.

### 186. Implement API key authentication

Extract the prefix and check hash, status, and expiration.

### 187. Implement API key scopes

Restrict allowed actions and resources.

### 188. Implement read-only mode

Prohibit mutation operations for read-only credentials.

### 189. Implement resource restrictions

Restrict the key to specific projects, organizations, or services.

### 190. Implement API key rotation

Create a new key and support a controlled overlap period.

### 191. Implement API key revocation

Immediately block use of a compromised credential.

### 192. Implement API key expiration

Support mandatory and configurable lifetime.

### 193. Implement last-used metadata

Save lastUsedAt, IP, and sanitized user agent.

### 194. Limit last-used writes

Do not update the database on every API request.

### 195. Implement service accounts

Create non-human identities for backend integrations.

### 196. Separate user and service-account permissions

Do not grant machine identity interactive user capabilities.

### 197. Implement API key rate limiting

Apply limits by credential and owner scope.

### 198. Implement API key audit

Record creation, rotation, use, denial, and revocation.

### 199. Implement secret scanning patterns

Allow CI and external scanners to detect the Authgate key format.

### 200. Test API key security

Check hashing, scopes, rotation, revocation, and prefix collisions.

## 11. OAuth 2.0 authorization server basics

### 201. Design the OAuthClient entity

Store clientId, type, redirect URIs, grants, scopes, and status.

### 202. Separate public and confidential clients

Do not issue a client secret to applications unable to store it securely.

### 203. Implement client registration

Create an OAuth client with validated metadata and policies.

### 204. Store client secrets as hashes

Show the raw secret only during creation or rotation.

### 205. Implement client secret rotation

Support a controlled overlap of multiple secrets.

### 206. Implement redirect URI validation

Require an exact match with the registered URI.

### 207. Design the AuthorizationCode entity

Store code hash, client, user, redirect URI, scopes, and expiration.

### 208. Implement Authorization Code Flow

Issue an authorization code after authentication and consent.

### 209. Implement PKCE

Support `S256` code challenge for public and confidential clients.

### 210. Prohibit implicit flow

Do not issue an access token through a browser redirect fragment.

### 211. Implement state validation guidance

Document mandatory use of state by the client application.

### 212. Implement authorization code one-time use

Atomically mark the code as used during token exchange.

### 213. Implement the token endpoint

Check client, grant, code, redirect URI, and PKCE verifier.

### 214. Implement Client Credentials Flow

Issue machine access tokens for service accounts.

### 215. Implement refresh token grant

Perform rotation and client binding.

### 216. Design OAuthScope

Store stable code, description, and allowed resource audiences.

### 217. Implement scope validation

Do not allow the client to request unregistered scopes.

### 218. Implement consent screen data

Provide client identity and requested permissions.

### 219. Implement consent persistence

Save user grants with the ability to revoke them.

### 220. Test OAuth grant flows

Check PKCE, redirect URI, code replay, scope escalation, and client authentication.

## 12. OpenID Connect and federation basics

### 221. Implement OpenID Provider metadata

Create a discovery endpoint with issuer, endpoints, and supported algorithms.

### 222. Implement ID Token

Issue a signed token with subject, audience, authTime, and nonce.

### 223. Check nonce

Bind the authentication request and ID Token to prevent replay.

### 224. Implement the UserInfo endpoint

Return claims within granted scopes.

### 225. Support standard OIDC scopes

Implement openid, profile, email, and offline_access.

### 226. Implement pairwise subject identifiers

Do not expose one global user identifier to all clients.

### 227. Implement the auth_time claim

Allow clients to require recent authentication.

### 228. Implement max_age

Request repeated authentication after a specified time.

### 229. Implement prompt behavior

Support login, consent, and none semantics.

### 230. Implement the acr claim

Transmit the achieved authentication assurance level.

### 231. Implement the amr claim

Transmit the authentication methods used.

### 232. Create an external IdP abstraction

Support OIDC identity providers through a separate adapter.

### 233. Implement external OIDC login

Check issuer, signature, nonce, state, and redirect context.

### 234. Implement identity linking

Link the external subject to an internal User through a confirmed process.

### 235. Prohibit unsafe email-based linking

Do not merge accounts solely by an unverified email claim.

### 236. Implement external identity unlinking

Do not allow removal of the last available authentication method.

### 237. Implement JIT user provisioning

Create an internal identity on the first successful external login.

### 238. Implement external identity audit

Record linking, login, unlinking, and provider errors.

### 239. Create an identity provider simulator

Generate valid, expired, replayed, and malformed OIDC responses.

### 240. Test federation flows

Check account linking, nonce, state, key rotation, and provider outage.

## 13. RBAC

### 241. Design the Permission entity

Store stable code, resource type, action, and description.

### 242. Create a permission naming convention

Use the `resource.action` format.

### 243. Design the Role entity

Store name, type, status, scope, and metadata.

### 244. Separate system and custom roles

Protect built-in roles from dangerous modification.

### 245. Design the RolePermission relation

Link roles to immutable permission codes.

### 246. Design RoleAssignment

Link subject, role, and scope.

### 247. Support global roles

Assign platform-level administrative permissions.

### 248. Support organization roles

Restrict assignment to a specific organization.

### 249. Support project roles

Restrict assignment to a specific project.

### 250. Implement role hierarchy

Inherit permissions with protection against cycles.

### 251. Implement custom role creation

Allow authorized administrators to create permission sets.

### 252. Implement role update

Modify permissions with optimistic locking.

### 253. Implement role archive

Prohibit new assignments without deleting history.

### 254. Prohibit deletion of a role in use

Require assignment migration.

### 255. Implement assignment expiration

Support temporary roles.

### 256. Implement bulk assignments

Assign roles to multiple subjects with a per-item result.

### 257. Implement effective permissions

Calculate the subject's final set of permissions within the scope.

### 258. Implement permission cache

Cache effective permissions with version-based invalidation.

### 259. Implement authorization explanation

Show through which role and assignment a permission was granted.

### 260. Test the RBAC matrix

Check roles, scopes, inheritance, expiration, and cache invalidation.

## 14. ABAC and policy engine

### 261. Design SubjectAttributes

Add identity type, roles, assurance level, and organizational attributes.

### 262. Design ResourceAttributes

Add owner, tenant, classification, status, and sensitivity.

### 263. Design EnvironmentAttributes

Add time, IP, network zone, device trust, and request channel.

### 264. Create the Policy entity

Store effect, actions, resource types, conditions, and version.

### 265. Implement a policy parser

Transform the stored representation into a safe executable model.

### 266. Prohibit dynamic code execution

Do not use `eval` and arbitrary JavaScript for policies.

### 267. Implement condition operators

Support equality, membership, comparison, CIDR, and time-window checks.

### 268. Implement allow policies

Grant access only when required conditions match.

### 269. Implement explicit deny

Define deny priority over allow.

### 270. Implement default deny

Reject the request when there is no matching allow policy.

### 271. Implement a policy combining algorithm

Record deny-overrides or another deterministic algorithm.

### 272. Implement policy versioning

Preserve the history of authorization rule changes.

### 273. Implement policy activation

Separate draft, active, and archived versions.

### 274. Implement policy simulation

Check the decision without applying the new policy.

### 275. Implement policy diff

Show changes in effective access.

### 276. Implement PolicyDecision

Return effect, matched policies, reason, and obligations.

### 277. Implement obligations

Require MFA, masking, or additional audit for an allowed action.

### 278. Implement policy cache

Cache compiled policies with a version key.

### 279. Research OPA and Cedar

Compare external policy engines with an embedded implementation.

### 280. Test ABAC policies

Check attributes, deny precedence, simulation, and malformed policies.

## 15. Backend access control patterns

### 281. Create AuthenticationContext

Pass subject, session, token, assurance, and client metadata.

### 282. Create AuthorizationContext

Pass subject, action, resource, and environment attributes.

### 283. Implement AuthenticationGuard

Check supported authentication mechanisms and credential status.

### 284. Implement PermissionGuard

Check required permissions at the controller boundary.

### 285. Implement PolicyGuard

Perform ABAC evaluation at the controller boundary.

### 286. Do not limit authorization to guards

Repeat the critical check inside the application use case.

### 287. Implement resource-level authorization

Load resource attributes before performing a mutation.

### 288. Protect against IDOR

Do not consider knowledge of a resource identifier proof of access.

### 289. Implement ownership policies

Allow restricted actions to the resource owner.

### 290. Implement scope decorators

Declare required scopes and permissions without business logic in metadata.

### 291. Implement composite authorization

Combine permission, ownership, assurance, and resource state checks.

### 292. Implement field-level authorization

Hide sensitive response fields according to policy.

### 293. Implement action-level masking

Restrict available transitions for a specific subject.

### 294. Implement batch authorization

Efficiently check a list of resources without N+1 policy calls.

### 295. Implement authorization filtering

Return only resources accessible to the caller.

### 296. Do not filter the full dataset in memory

Apply authorization scope at the query level.

### 297. Implement service-to-service authorization

Check service identity, audience, and machine scopes.

### 298. Implement delegated access

Support a restricted action on behalf of a user.

### 299. Implement impersonation

Store the real actor, impersonated subject, scope, and expiration.

### 300. Test access control patterns

Check guards, use cases, query filtering, field masking, and impersonation.

## 16. Rate limiting and abuse prevention

### 301. Define rate-limit dimensions

Separate IP, user, session, API key, client, and endpoint limits.

### 302. Implement a fixed-window limiter

Create a basic implementation for non-critical endpoints.

### 303. Implement a sliding-window limiter

Provide more even request limiting.

### 304. Implement token bucket

Support burst capacity and a sustained rate.

### 305. Implement a Redis-backed limiter

Provide consistent limiting across instances.

### 306. Use atomic Redis operations

Eliminate race conditions during increment and expiration.

### 307. Implement login rate limiting

Limit attempts by IP and normalized identity.

### 308. Implement distributed password spraying detection

Detect attempts to use one password against multiple users.

### 309. Implement credential stuffing detection

Detect large-scale attempts using known credentials.

### 310. Implement reset rate limiting

Limit email, IP, and device dimensions.

### 311. Implement verification resend limits

Prevent spam and email abuse.

### 312. Implement OAuth endpoint limits

Limit authorization, token, and introspection requests.

### 313. Implement API key limits

Apply per-key and per-owner quotas.

### 314. Implement adaptive throttling

Tighten limits when the risk score is suspicious.

### 315. Implement progressive delay

Increase the delay after repeated authentication failures.

### 316. Avoid permanent account lockout

Do not allow an attacker to lock another identity with simple attempts.

### 317. Implement CAPTCHA abstraction

Connect a challenge only for an elevated risk level.

### 318. Implement abuse event publishing

Send security signals to the audit and alerting pipeline.

### 319. Implement rate-limit headers

Return limit, remaining, and retry time without exposing security policy.

### 320. Test abuse controls

Check concurrency, distributed limits, bypass attempts, and Redis outage.

## 17. Audit logging and security events

### 321. Design AuditEvent

Store actor, action, target, outcome, timestamp, and context.

### 322. Separate audit and application logs

Do not use regular logs as authoritative security history.

### 323. Implement append-only audit storage

Prohibit update and delete through the runtime application role.

### 324. Record authentication events

Store login success, failure, logout, and session revocation.

### 325. Record credential events

Store password change, reset, MFA enrollment, and recovery.

### 326. Record authorization events

Store critical allow and deny decisions.

### 327. Record role events

Store role creation, permission changes, and assignments.

### 328. Record API key events

Store creation, rotation, use, and revocation.

### 329. Record OAuth events

Store consent, code issuance, token issuance, and client failures.

### 330. Record impersonation events

Store the real actor, target identity, and performed actions.

### 331. Add request context

Store requestId, traceId, IP, user agent, and clientId.

### 332. Sanitize audit metadata

Remove passwords, raw tokens, secrets, and sensitive claims.

### 333. Implement an audit integrity chain

Link record hashes to detect modification of history.

### 334. Implement audit retention

Configure retention periods by event type and compliance requirements.

### 335. Implement an audit search API

Add filtering by actor, action, target, outcome, and time.

### 336. Implement audit export

Export records to JSON or CSV with a checksum.

### 337. Implement security event severity

Classify informational, warning, high, and critical events.

### 338. Implement security notifications

Notify the user about password reset, new device, and API key creation.

### 339. Implement alert triggers

Create alerts for token reuse, privilege escalation, and brute force.

### 340. Test audit completeness

Check for events for all critical security operations.

## 18. Cryptography, secrets, and key management

### 341. Create a cryptographic inventory

Record algorithms, keys, purposes, owners, and rotation periods.

### 342. Separate signing and encryption keys

Do not use one key for different cryptographic purposes.

### 343. Implement a key abstraction

Isolate application code from local files, KMS, and HSM.

### 344. Implement envelope encryption

Encrypt sensitive values with data keys protected by a master key.

### 345. Encrypt TOTP secrets

Store MFA secrets in encrypted form.

### 346. Encrypt external provider tokens

Protect refresh tokens and client credentials of federation providers.

### 347. Implement signing key rotation

Publish new public keys before starting to use the private key.

### 348. Implement encryption key rotation

Re-encrypt sensitive data without full downtime.

### 349. Implement secret versioning

Store the key version next to the encrypted payload.

### 350. Implement secret loading

Retrieve production secrets from protected storage.

### 351. Prohibit secrets in the repository

Add secret scanning to pre-commit and CI.

### 352. Prohibit secrets in logs

Implement centralized redaction.

### 353. Implement secure random generation

Use an operating-system CSPRNG for tokens and keys.

### 354. Implement constant-time comparisons

Use secure comparison functions for signatures and hashes.

### 355. Configure TLS

Use modern protocol versions and certificate validation.

### 356. Implement mTLS for internal clients

Authenticate trusted service-to-service connections.

### 357. Implement a key compromise procedure

Prepare emergency rotation and token invalidation.

### 358. Implement cryptographic health checks

Check for active keys without exposing secret material.

### 359. Create cryptographic test vectors

Check signing, verification, encryption, and rotation.

### 360. Document the key management lifecycle

Describe generation, distribution, activation, rotation, revocation, and destruction.

## 19. Asynchronous workflows and messaging

### 361. Create an integration event envelope

Add eventId, type, version, occurredAt, subject, and correlationId.

### 362. Separate domain and integration events

Do not publish internal entities directly.

### 363. Implement transactional outbox

Atomically save auth state and the integration event.

### 364. Implement an outbox publisher

Publish events through RabbitMQ with confirms and retries.

### 365. Implement outbox locking

Use `FOR UPDATE SKIP LOCKED`.

### 366. Implement outbox cleanup

Archive published records according to the retention policy.

### 367. Implement inbox deduplication

Do not process the integration event repeatedly.

### 368. Implement email jobs

Send verification, reset, and security notifications asynchronously.

### 369. Implement job idempotency

Do not send duplicate email on retry.

### 370. Implement delayed jobs

Process token cleanup and scheduled session expiration.

### 371. Implement retry policy

Retry transient failures with exponential backoff and jitter.

### 372. Implement a dead-letter queue

Isolate unprocessable events and jobs.

### 373. Implement dead-letter inspection

Show event type, subject, attempts, and failure reason.

### 374. Implement selective redrive

Rerun corrected jobs with an audit trail.

### 375. Implement a session cleanup job

Delete or archive expired session records.

### 376. Implement a token cleanup job

Delete expired verification, reset, and refresh token records.

### 377. Implement compromised credential notification

Asynchronously notify downstream services about revocation.

### 378. Implement authorization cache invalidation events

Invalidate permissions after role changes.

### 379. Implement event contract versioning

Support backward-compatible evolution.

### 380. Test asynchronous workflows

Check retries, duplicate delivery, crash recovery, and DLQ.

## 20. Persistence and data model

### 381. Design the PostgreSQL schema

Create users, credentials, sessions, tokens, API keys, roles, policies, and audit events tables.

### 382. Use database constraints

Enforce uniqueness, required relations, and valid status combinations.

### 383. Add a unique email index

Use a normalized email representation.

### 384. Add credential constraints

Prohibit multiple active password credentials under the selected model.

### 385. Add session indexes

Optimize lookup by userId, status, and expiresAt.

### 386. Add refresh token indexes

Optimize lookup by hash, familyId, and sessionId.

### 387. Add an API key prefix index

Accelerate credential lookup.

### 388. Add role assignment indexes

Optimize effective-permission queries.

### 389. Add audit indexes

Support search by actor, target, and timestamp.

### 390. Implement optimistic locking

Add version for User, Role, Policy, and OAuthClient.

### 391. Implement pessimistic locking

Use row locks for token rotation and one-time code consumption.

### 392. Configure transaction isolation

Choose an isolation level for credential and authorization operations.

### 393. Implement transaction retries

Retry serialization failures without repeating external side effects.

### 394. Separate runtime and migration roles

Do not grant the application permission to modify the schema.

### 395. Restrict database privileges

Grant each process the minimum set of permissions.

### 396. Implement a soft-delete query policy

Do not return deactivated and deleted identities from regular repositories.

### 397. Implement data retention jobs

Delete expired operational records according to policy.

### 398. Implement database backup

Configure point-in-time recovery.

### 399. Test restore

Restore the auth database and check cryptographic compatibility.

### 400. Document data ownership

Record authoritative tables and derived cache data.

## 21. Unit and integration testing

### 401. Create unit tests for the User state machine

Check activation, suspension, lock, and deactivation.

### 402. Create unit tests for the Email value object

Check normalization and invalid formats.

### 403. Create unit tests for the password policy

Check length, breach detection, and history.

### 404. Create unit tests for password hashing

Check verification and parameter migration.

### 405. Create unit tests for the Session state machine

Check expiration, revocation, and rotation.

### 406. Create unit tests for the RefreshToken family

Check rotation, reuse detection, and family revocation.

### 407. Create unit tests for API keys

Check scopes, expiration, and status.

### 408. Create unit tests for OAuth codes

Check expiration, PKCE, and one-time consumption.

### 409. Create unit tests for RBAC

Check roles, hierarchy, and scope inheritance.

### 410. Create unit tests for ABAC

Check condition operators and deny precedence.

### 411. Create unit tests for rate limiting

Check windows, bursts, and expiration.

### 412. Create unit tests for audit sanitization

Check removal of sensitive fields.

### 413. Create architecture tests

Check layers, modules, and prohibited dependencies.

### 414. Configure Testcontainers PostgreSQL

Run integration tests against a real database version.

### 415. Configure Testcontainers Redis

Check sessions, rate limits, and cache invalidation.

### 416. Configure Testcontainers RabbitMQ

Check outbox, email jobs, and security events.

### 417. Create repository integration tests

Check constraints, locks, and transaction behavior.

### 418. Create session integration tests

Check cookies, Redis cache, and PostgreSQL source of truth.

### 419. Create token integration tests

Check signing, JWKS, rotation, and introspection.

### 420. Create authorization integration tests

Check guards, use cases, query filtering, and cache invalidation.

## 22. Security testing

### 421. Create authentication end-to-end tests

Check registration, verification, login, refresh, and logout.

### 422. Create password reset end-to-end tests

Check request, completion, revocation, and notification.

### 423. Create MFA end-to-end tests

Check enrollment, challenge, recovery, and step-up.

### 424. Create API key end-to-end tests

Check creation, use, rotation, and revocation.

### 425. Create OAuth Authorization Code tests

Check redirect URI, state, PKCE, and code replay.

### 426. Create Client Credentials tests

Check client authentication, audience, and scopes.

### 427. Create OIDC tests

Check nonce, ID Token, UserInfo, and discovery metadata.

### 428. Test user enumeration

Check login, registration, reset, and verification responses.

### 429. Test session fixation

Check identifier rotation after authentication.

### 430. Test CSRF

Check cookie-authenticated mutation endpoints.

### 431. Test token replay

Reuse authorization codes, reset tokens, and rotated refresh tokens.

### 432. Test JWT attacks

Check algorithm confusion, invalid kid, wrong audience, and expired tokens.

### 433. Test IDOR

Use identifiers of other users' sessions, keys, roles, and clients.

### 434. Test privilege escalation

Attempt to assign a role or scope to oneself without permission.

### 435. Test policy bypass

Check missing attributes, malformed conditions, and cache staleness.

### 436. Test brute force controls

Check distributed login attempts and rate-limit evasion.

### 437. Test race conditions

Use a refresh token, reset token, and authorization code concurrently.

### 438. Test timing differences

Compare response times for existing and unknown identities.

### 439. Perform a dependency security scan

Check libraries, container images, and transitive dependencies.

### 440. Create a security regression suite

Run critical authentication and authorization tests in CI.

## 23. Performance and reliability

### 441. Define performance targets

Record p95 login, session validation, token issuance, and authorization latency.

### 442. Create a login load test

Measure hashing cost, database load, and rate limiting.

### 443. Create a session validation load test

Check PostgreSQL and Redis-backed models.

### 444. Create a token issuance load test

Measure signing throughput and key access overhead.

### 445. Create a JWKS load test

Check caching and high-volume resource-server access.

### 446. Create an authorization load test

Measure RBAC, ABAC, and combined policy evaluation.

### 447. Create an API key authentication load test

Measure prefix lookup and hash verification.

### 448. Create an OAuth token endpoint load test

Check code exchange and refresh rotation concurrency.

### 449. Optimize database indexes

Use `EXPLAIN ANALYZE` for critical queries.

### 450. Optimize password hashing concurrency

Do not block the event loop or exhaust the worker pool.

### 451. Move CPU-bound crypto out

Use worker threads or a controlled native implementation when necessary.

### 452. Implement authorization cache

Cache roles and policies with safe invalidation.

### 453. Implement JWKS cache

Cache public keys in resource services.

### 454. Implement cache stampede protection

Prevent massive simultaneous loading of permissions and keys.

### 455. Implement a circuit breaker

Isolate email, external IdP, and KMS failures.

### 456. Implement a timeout policy

Limit database, Redis, provider, and KMS calls.

### 457. Implement graceful degradation

Preserve local authentication when optional providers are unavailable.

### 458. Perform a soak test

Detect memory leaks, session growth, and connection leaks.

### 459. Perform dependency outage tests

Disable Redis, RabbitMQ, email provider, and external IdP.

### 460. Create a capacity model

Calculate instances, database, Redis, and cryptographic throughput.

## 24. Observability

### 461. Implement structured logging

Add service, environment, requestId, traceId, userId, and sessionId.

### 462. Pseudonymize identity data

Do not write raw email and tokens to logs.

### 463. Implement centralized redaction

Remove passwords, cookies, authorization headers, and secrets.

### 464. Implement OpenTelemetry tracing

Trace HTTP, database, Redis, messaging, and external providers.

### 465. Add authentication spans

Measure lookup, password verification, MFA, and session creation.

### 466. Add authorization spans

Measure policy evaluation and cache operations.

### 467. Add token spans

Measure signing, verification, introspection, and rotation.

### 468. Add authentication metrics

Collect successes, failures, lockouts, and MFA challenges.

### 469. Add session metrics

Collect active, created, revoked, and expired sessions.

### 470. Add token metrics

Collect issued, refreshed, reused, and revoked tokens.

### 471. Add API key metrics

Collect authentications, failures, expirations, and revocations.

### 472. Add OAuth metrics

Collect authorization, token grants, failures, and consent events.

### 473. Add authorization metrics

Collect allow, deny, evaluation duration, and cache hit rate.

### 474. Add rate-limit metrics

Collect blocked requests by endpoint and credential type.

### 475. Add audit metrics

Collect ingestion rate, export failures, and integrity errors.

### 476. Create a Grafana authentication dashboard

Show login rates, failures, MFA, and sessions.

### 477. Create a Grafana authorization dashboard

Show decisions, latency, and cache performance.

### 478. Create a Grafana security dashboard

Show brute force, token reuse, and privilege escalation events.

### 479. Configure alerts

Create alerts for login failure spikes, token reuse, and signing-key failures.

### 480. Define Authgate SLI and SLO

Record availability, authentication latency, and authorization correctness indicators.

## 25. Deployment and operations

### 481. Create production Dockerfiles

Use a multi-stage build, non-root user, and minimal runtime image.

### 482. Separate API and worker deployments

Scale synchronous and asynchronous workloads independently.

### 483. Configure resource limits

Limit CPU and memory for API and workers.

### 484. Configure rolling deployments

Preserve sessions and token validation during instance updates.

### 485. Implement graceful draining

Complete active authentication requests before shutdown.

### 486. Create a migration policy

Use expand-migrate-contract for backward-compatible schema changes.

### 487. Implement zero-downtime key rotation

Update signing keys without verification failure.

### 488. Implement zero-downtime cookie changes

Support transition between cookie names and secrets.

### 489. Configure autoscaling

Scale the API by latency, CPU, and request rate.

### 490. Limit autoscaling

Do not overload PostgreSQL, Redis, and KMS.

### 491. Configure PostgreSQL backup

Provide point-in-time recovery.

### 492. Configure Redis persistence policy

Define recovery requirements for sessions and rate limits.

### 493. Create a disaster recovery plan

Describe recovery of database, keys, sessions, and OAuth clients.

### 494. Perform a disaster recovery test

Restore the environment and check token verification.

### 495. Create a runbook for a login failure spike

Describe diagnostics for credentials, dependencies, and attack traffic.

### 496. Create a runbook for a token reuse incident

Describe revocation, user notification, and forensic analysis.

### 497. Create a runbook for signing-key compromise

Describe emergency rotation and mass token invalidation.

### 498. Create a runbook for external IdP outage

Describe fallback and communication procedures.

### 499. Create a runbook for Redis outage

Describe session validation and rate-limit fallback.

### 500. Create a runbook for an authorization incident

Describe containment, policy rollback, and audit investigation.

## 26. Documentation and production-style scenarios

### 501. Create the repository README

Describe Authgate's purpose, architecture, startup, and main flows.

### 502. Create a C4 System Context diagram

Show users, clients, resource services, and external identity providers.

### 503. Create a C4 Container diagram

Show Auth API, workers, PostgreSQL, Redis, broker, and KMS.

### 504. Create component diagrams

Show Identity, Sessions, Tokens, OAuth, Authorization, and Audit modules.

### 505. Create a password login sequence diagram

Show credential verification, MFA, session, and token issuance.

### 506. Create a refresh rotation sequence diagram

Show token family, reuse detection, and revocation.

### 507. Create an OAuth flow sequence diagram

Show authorization, consent, PKCE, and token exchange.

### 508. Create an API key authentication sequence diagram

Show prefix lookup, hash verification, scopes, and audit.

### 509. Create an authorization sequence diagram

Show context building, RBAC, ABAC, and decision enforcement.

### 510. Document authentication state machines

Describe User, Session, RefreshToken, and MFA states.

### 511. Document the authorization model

Describe roles, permissions, scopes, policies, and decision precedence.

### 512. Document the token model

Describe claims, lifetime, rotation, introspection, and revocation.

### 513. Create an ADR for session strategy

Justify server-side sessions, JWT, or a hybrid model.

### 514. Create an ADR for password hashing

Record the algorithm, parameters, and upgrade strategy.

### 515. Create an ADR for authorization architecture

Justify RBAC, ABAC, and policy engine boundaries.

### 516. Implement production-style browser authentication

Show registration, verification, login, MFA, cookie session, and logout.

### 517. Implement a production-style token flow

Show access token, refresh rotation, reuse attack, and family revocation.

### 518. Implement production-style machine access

Show service account, API key, OAuth Client Credentials, and scoped authorization.

### 519. Implement a production-style security incident

Simulate credential compromise, revoke credentials, and restore access.

### 520. Prepare a production readiness checklist

Record mandatory checks for authentication, authorization, cryptography, observability, recovery, and operations.
