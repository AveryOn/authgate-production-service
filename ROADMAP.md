# Authgate Production Service Roadmap

## 1. Основы authentication и authorization

### 001. Разделить authentication и authorization

Зафиксировать различия между установлением identity пользователя и проверкой его права выполнить конкретное действие.

### 002. Исследовать identity lifecycle

Разобрать регистрацию, верификацию, активацию, suspension, recovery, deactivation и удаление identity.

### 003. Исследовать credential lifecycle

Разобрать создание, ротацию, компрометацию, отзыв и истечение credentials.

### 004. Исследовать session-based authentication

Определить модель server-side sessions, session identifiers, cookies и session storage.

### 005. Исследовать token-based authentication

Разобрать access tokens, refresh tokens, bearer semantics и ограничения stateless authentication.

### 006. Сравнить opaque и self-contained tokens

Зафиксировать различия introspection, revocation, latency, payload exposure и key management.

### 007. Исследовать authentication assurance levels

Определить уровни доверия для password, MFA, WebAuthn и step-up authentication.

### 008. Исследовать RBAC

Разобрать users, roles, permissions, assignments и role hierarchy.

### 009. Исследовать ABAC

Разобрать subject, resource, action, environment attributes и policy evaluation.

### 010. Исследовать ACL

Определить случаи использования resource-level access control lists.

### 011. Исследовать ReBAC

Разобрать доступ на основании отношений user, team, organization и resource.

### 012. Исследовать policy-based authorization

Определить структуру policies, decisions, obligations и deny reasons.

### 013. Исследовать OAuth 2.0

Разобрать resource owner, client, authorization server, resource server и authorization grants.

### 014. Исследовать OpenID Connect

Определить назначение ID Token, UserInfo и identity claims поверх OAuth 2.0.

### 015. Исследовать Zero Trust

Зафиксировать принцип постоянной проверки identity, device, context и requested action.

### 016. Исследовать defense in depth

Определить уровни защиты на transport, application, data и operational layers.

### 017. Исследовать least privilege

Запретить выдачу credentials и permissions шире необходимого scope.

### 018. Исследовать confused deputy problem

Разобрать ситуации, когда доверенный backend выполняет действие от имени недостаточно авторизованного caller.

### 019. Определить trust boundaries

Зафиксировать границы между browser, API, auth service, resource services, database и external identity providers.

### 020. Зафиксировать security invariants

Документировать обязательные правила credential storage, session validation, authorization и audit.

## 2. Структура репозитория и инфраструктура

### 021. Создать monorepo

Настроить workspace для Auth API, background workers, administration CLI и shared libraries.

### 022. Создать NestJS Auth API

Реализовать основное HTTP-приложение для authentication, sessions, API keys и authorization.

### 023. Создать background worker

Выделить отдельный процесс для email, cleanup, audit export и security notifications.

### 024. Создать administration CLI

Добавить команды управления users, sessions, keys, roles и security incidents.

### 025. Определить shared libraries

Выделить domain, application, contracts, database, crypto, observability и testing packages.

### 026. Настроить TypeScript strict mode

Включить строгую проверку типов, nullability и unsafe operations.

### 027. Настроить project references

Разделить сборку приложений и библиотек с контролируемыми dependencies.

### 028. Настроить path aliases

Создать стабильные aliases для domain, application, adapters и shared packages.

### 029. Настроить ESLint

Добавить правила для Promise handling, security-sensitive code и запрещённых imports.

### 030. Настроить Prettier

Обеспечить единый формат TypeScript, JSON, YAML и Markdown.

### 031. Настроить environment validation

Проверять PostgreSQL, Redis, RabbitMQ, signing keys, cookie settings и email provider configuration.

### 032. Создать Docker Compose окружение

Добавить PostgreSQL, Redis, RabbitMQ, Mailpit и observability stack.

### 033. Настроить PostgreSQL migrations

Создать воспроизводимый migration workflow для development, test и production.

### 034. Создать development seeds

Подготовить users, roles, permissions, sessions, clients и API keys.

### 035. Настроить application bootstrap

Подключить validation, error handling, security headers, logging и tracing.

### 036. Реализовать liveness endpoint

Проверять работоспособность процесса без обращения к внешним dependencies.

### 037. Реализовать readiness endpoint

Проверять PostgreSQL, Redis, broker и обязательные cryptographic materials.

### 038. Реализовать graceful shutdown

Корректно завершать HTTP-запросы, workers, consumers и database connections.

### 039. Настроить configuration profiles

Разделить development, test, staging и production settings.

### 040. Создать local quick-start script

Автоматизировать запуск infrastructure, migrations, seeds и applications.

## 3. Архитектура и domain boundaries

### 041. Определить Authgate modules

Выделить Identity, Credentials, Sessions, Tokens, API Keys, Authorization, OAuth и Audit.

### 042. Определить bounded contexts

Зафиксировать ответственность и ownership данных каждого module.

### 043. Спроектировать Hexagonal Architecture

Разделить domain, application, ports, adapters, delivery и infrastructure layers.

### 044. Определить aggregate boundaries

Выделить User, Credential, Session, APIKey, OAuthClient, Role и Policy aggregates.

### 045. Создать domain layer

Разместить entities, value objects, domain services, policies и events без framework dependencies.

### 046. Создать application layer

Разместить use cases, commands, queries, ports и transaction orchestration.

### 047. Создать infrastructure layer

Реализовать PostgreSQL, Redis, crypto, messaging и external identity adapters.

### 048. Создать delivery layer

Реализовать HTTP controllers, CLI commands и broker consumers.

### 049. Определить repository ports

Изолировать application layer от ORM и database implementation.

### 050. Определить TransactionPort

Позволить use cases выполнять atomic operations без зависимости от ORM.

### 051. Определить PasswordHasherPort

Изолировать password hashing algorithm от domain logic.

### 052. Определить TokenSignerPort

Изолировать JWT и opaque token generation от use cases.

### 053. Определить SessionStorePort

Поддержать PostgreSQL, Redis или hybrid session storage.

### 054. Определить EmailSenderPort

Отделить verification и reset notifications от email provider.

### 055. Определить ClockPort

Обеспечить детерминированное тестирование expiration и rotation.

### 056. Определить RandomGeneratorPort

Использовать cryptographically secure identifiers и secrets.

### 057. Использовать explicit DI tokens

Не полагаться на runtime TypeScript interfaces для dependency injection.

### 058. Запретить infrastructure imports в domain

Добавить автоматические architecture checks.

### 059. Запретить deep imports между modules

Экспортировать только публичные contracts и application ports.

### 060. Документировать dependency direction

Зафиксировать допустимые зависимости между layers и modules.

## 4. Identity model и user lifecycle

### 061. Спроектировать User entity

Добавить id, status, primaryEmail, timestamps и security metadata.

### 062. Создать UserId value object

Исключить случайное смешивание user identifiers с другими IDs.

### 063. Создать Email value object

Добавить normalization, validation и case-insensitive comparison.

### 064. Определить email uniqueness policy

Зафиксировать глобальную uniqueness и правила повторного использования адресов.

### 065. Разделить User и UserProfile

Отделить authentication identity от display name и application-specific данных.

### 066. Реализовать User status machine

Поддержать pending, active, locked, suspended, deactivated и deleted states.

### 067. Реализовать user registration

Создавать pending identity с неподтверждённым email.

### 068. Реализовать registration idempotency

Не создавать duplicate users при повторном request.

### 069. Реализовать account activation

Активировать identity после выполнения обязательных verification steps.

### 070. Реализовать account suspension

Блокировать authentication без удаления credentials и audit history.

### 071. Реализовать account reactivation

Восстанавливать доступ после административного решения.

### 072. Реализовать account lock

Временно блокировать authentication после security event.

### 073. Реализовать account unlock

Поддержать automatic и administrative unlock.

### 074. Реализовать account deactivation

Отзывать sessions, refresh tokens и API keys пользователя.

### 075. Реализовать account deletion request

Создавать управляемый workflow с retention period.

### 076. Реализовать soft deletion

Скрывать identity из обычных queries без физического удаления security records.

### 077. Реализовать account anonymization

Удалять необязательные PII без повреждения audit и authorization history.

### 078. Реализовать identity merge policy

Определить безопасное объединение duplicate identities.

### 079. Создать user lifecycle events

Публиковать UserRegistered, UserActivated, UserSuspended и UserDeactivated.

### 080. Тестировать user lifecycle invariants

Проверить допустимые transitions и обязательный credential revocation.

## 5. Password credentials

### 081. Спроектировать PasswordCredential entity

Хранить userId, passwordHash, algorithm, parameters и timestamps.

### 082. Использовать Argon2id

Настроить memory cost, time cost и parallelism для production environment.

### 083. Исследовать bcrypt и scrypt

Сравнить свойства algorithms и зафиксировать причины выбора Argon2id.

### 084. Создать password hashing benchmark

Подобрать параметры hashing по security и latency targets.

### 085. Реализовать per-password salt

Использовать уникальный cryptographic salt для каждого credential.

### 086. Реализовать pepper

Добавить application-level secret отдельно от database.

### 087. Реализовать password verification

Сравнивать hashes через безопасную library implementation.

### 088. Реализовать hash parameter upgrade

Перехешировать password после успешного login при устаревших параметрах.

### 089. Реализовать password policy

Проверять минимальную длину и запрещённые категории credentials.

### 090. Не ограничивать password composition искусственными правилами

Не требовать обязательные символы, снижающие реальную entropy через предсказуемые patterns.

### 091. Проверять compromised passwords

Интегрировать локальный или внешний breach dataset.

### 092. Реализовать password history

Запрещать повторное использование последних credentials при необходимости policy.

### 093. Реализовать password change

Требовать текущий password или step-up authentication.

### 094. Реализовать forced password change

Поддержать administrative requirement без хранения temporary plaintext password.

### 095. Инвалидировать sessions после password change

Завершать выбранные или все sessions согласно security policy.

### 096. Реализовать credential version

Увеличивать version при password change для token invalidation.

### 097. Реализовать password expiration policy

Поддержать configurable expiration только для environments, где это требуется.

### 098. Защитить password endpoints

Добавить rate limiting, audit и sensitive-field redaction.

### 099. Реализовать constant-shape login response

Не раскрывать существование пользователя через различающиеся messages.

### 100. Тестировать password credential security

Проверить hashing, migration, reuse, timing и invalidation scenarios.

## 6. Email verification и password reset

### 101. Спроектировать VerificationToken entity

Хранить token hash, purpose, userId, expiresAt, usedAt и metadata.

### 102. Генерировать cryptographically secure tokens

Использовать достаточную entropy и URL-safe encoding.

### 103. Хранить verification tokens как hashes

Не сохранять raw token в database.

### 104. Реализовать email verification request

Создавать одноразовый token и отправлять verification link.

### 105. Реализовать email verification completion

Проверять hash, purpose, expiration и usage state.

### 106. Реализовать verification token rotation

Инвалидировать предыдущий active token при повторной отправке.

### 107. Реализовать verification resend

Добавить cooldown и rate limiting.

### 108. Реализовать verification expiration

Отклонять просроченные tokens с безопасным error response.

### 109. Реализовать email change request

Требовать подтверждение нового email и step-up authentication.

### 110. Реализовать email change completion

Атомарно обновлять primaryEmail и invalidation metadata.

### 111. Спроектировать PasswordResetRequest

Хранить token hash, userId, expiresAt, usedAt и request context.

### 112. Реализовать password reset request

Возвращать одинаковый response для существующего и неизвестного email.

### 113. Реализовать password reset completion

Проверять token и обновлять credential в одной transaction.

### 114. Инвалидировать reset token после использования

Запрещать replay успешного reset request.

### 115. Инвалидировать старые reset tokens

Отзывать все незавершённые tokens после успешной смены password.

### 116. Отзывать sessions после password reset

Завершать существующие sessions и refresh token families.

### 117. Отправлять security notification

Уведомлять пользователя о password change и reset completion.

### 118. Реализовать reset abuse protection

Ограничивать частоту requests по email, IP и device fingerprint.

### 119. Добавить audit для verification и reset

Фиксировать request, success, failure и token replay.

### 120. Тестировать recovery flows

Проверить expiration, duplicate requests, replay и concurrent completion.

## 7. Sessions и cookies

### 121. Спроектировать Session entity

Хранить sessionId, userId, status, createdAt, lastSeenAt и expiresAt.

### 122. Хранить session identifiers как hashes

Не сохранять raw session cookie в database.

### 123. Генерировать secure session identifiers

Использовать cryptographically secure random values.

### 124. Реализовать session creation

Создавать session только после успешной authentication.

### 125. Реализовать session validation

Проверять status, expiration, user status и credential version.

### 126. Реализовать absolute expiration

Ограничивать максимальный срок жизни session.

### 127. Реализовать idle expiration

Завершать session после периода неактивности.

### 128. Реализовать sliding expiration

Продлевать session в пределах absolute lifetime.

### 129. Реализовать last-seen throttling

Не обновлять session record на каждый request.

### 130. Реализовать session rotation

Менять session identifier после login и privilege elevation.

### 131. Защититься от session fixation

Никогда не сохранять pre-authentication session identifier после login.

### 132. Настроить secure cookies

Использовать HttpOnly, Secure, SameSite и ограниченный Path.

### 133. Определить cookie domain policy

Не расширять cookie scope на лишние subdomains.

### 134. Реализовать CSRF protection

Использовать synchronizer token или double-submit pattern для cookie auth.

### 135. Реализовать session revocation

Позволить завершить одну выбранную session.

### 136. Реализовать revoke-all sessions

Завершать все sessions пользователя кроме текущей или включая её.

### 137. Реализовать device session list

Показывать device metadata, location approximation и last activity.

### 138. Реализовать suspicious session detection

Фиксировать резкую смену device, ASN или geography.

### 139. Реализовать Redis session cache

Ускорить validation без потери authoritative PostgreSQL state.

### 140. Тестировать session lifecycle

Проверить rotation, expiration, revocation, CSRF и concurrent requests.

## 8. Access tokens и refresh tokens

### 141. Спроектировать AccessToken claims

Добавить subject, issuer, audience, issuedAt, expiresAt, sessionId и scopes.

### 142. Минимизировать JWT payload

Не включать PII и изменяемые authorization данные без необходимости.

### 143. Реализовать asymmetric token signing

Использовать RSA или ECDSA keys для отделения signing и verification.

### 144. Реализовать key identifiers

Добавлять `kid` для выбора verification key.

### 145. Создать JWKS endpoint

Публиковать активные public keys для resource services.

### 146. Реализовать signing key rotation

Поддерживать одновременно current и previous verification keys.

### 147. Проверять issuer и audience

Не принимать token, выпущенный для другого service или environment.

### 148. Проверять token lifetime

Валидировать exp, nbf и допустимый clock skew.

### 149. Проверять signature algorithm

Запрещать algorithm confusion и неподдерживаемые algorithms.

### 150. Спроектировать RefreshToken entity

Хранить token hash, familyId, sessionId, status и expiration.

### 151. Реализовать refresh token rotation

Выдавать новый token при каждом успешном refresh.

### 152. Реализовать refresh token reuse detection

Определять повторное использование уже rotated token.

### 153. Отзывать refresh token family

Завершать всю цепочку при обнаружении reuse.

### 154. Связать refresh token с session

Не позволять refresh после revocation или expiration session.

### 155. Реализовать refresh token absolute expiration

Ограничивать максимальный lifetime независимо от rotation.

### 156. Реализовать refresh token idle expiration

Завершать неиспользуемые token families.

### 157. Реализовать opaque refresh tokens

Не раскрывать внутренние claims в client-visible token.

### 158. Реализовать token introspection

Предоставить protected endpoint для проверки opaque или revocable token.

### 159. Реализовать token revocation endpoint

Позволить client отозвать refresh или access token reference.

### 160. Тестировать token lifecycle

Проверить rotation, reuse, key rollover, audience и revocation.

## 9. MFA, step-up authentication и passkeys

### 161. Спроектировать AuthenticationFactor

Поддержать password, TOTP, WebAuthn и recovery code types.

### 162. Реализовать MFA enrollment state

Разделить pending, active, suspended и revoked factor states.

### 163. Реализовать TOTP enrollment

Генерировать secret, provisioning URI и initial verification challenge.

### 164. Хранить TOTP secrets безопасно

Шифровать secrets at rest и ограничивать доступ application role.

### 165. Реализовать TOTP verification

Проверять допустимое временное окно и предотвращать replay одного code.

### 166. Реализовать TOTP removal

Требовать step-up authentication или recovery procedure.

### 167. Реализовать recovery codes

Генерировать одноразовые codes и хранить только hashes.

### 168. Реализовать recovery code consumption

Атомарно помечать code использованным.

### 169. Реализовать recovery code regeneration

Инвалидировать предыдущий набор после подтверждения identity.

### 170. Исследовать WebAuthn

Разобрать authenticator, credential, challenge, origin и relying party.

### 171. Реализовать WebAuthn registration

Проверять challenge, origin, RP ID и attestation result.

### 172. Реализовать WebAuthn authentication

Проверять assertion, signature counter и user presence.

### 173. Поддержать discoverable credentials

Реализовать passkey login без предварительного ввода username.

### 174. Обрабатывать cloned authenticator signals

Реагировать на некорректное изменение signature counter.

### 175. Реализовать MFA challenge entity

Хранить purpose, factor, expiration и attempt limits.

### 176. Реализовать step-up authentication

Повышать assurance level для критичных operations.

### 177. Реализовать remembered device

Создавать ограниченный trusted-device credential с expiration.

### 178. Реализовать MFA policy

Требовать MFA по role, tenant, risk level или operation.

### 179. Реализовать MFA recovery

Создать защищённый process без обхода existing factors.

### 180. Тестировать MFA flows

Проверить enrollment, replay, recovery, step-up и factor revocation.

## 10. API keys и machine credentials

### 181. Спроектировать APIKey entity

Хранить owner, prefix, hash, scopes, status и expiration.

### 182. Генерировать API key secret

Использовать cryptographically secure random value достаточной длины.

### 183. Хранить API keys как hashes

Показывать raw secret только один раз после создания.

### 184. Реализовать API key prefix

Использовать prefix для поиска key record и идентификации environment.

### 185. Реализовать API key creation

Проверять owner authorization, scopes и expiration policy.

### 186. Реализовать API key authentication

Извлекать prefix, проверять hash, status и expiration.

### 187. Реализовать API key scopes

Ограничивать разрешённые actions и resources.

### 188. Реализовать read-only mode

Запрещать mutation operations для read-only credentials.

### 189. Реализовать resource restrictions

Ограничивать key конкретными projects, organizations или services.

### 190. Реализовать API key rotation

Создавать новый key и поддерживать controlled overlap period.

### 191. Реализовать API key revocation

Немедленно блокировать использование compromised credential.

### 192. Реализовать API key expiration

Поддерживать обязательный и configurable lifetime.

### 193. Реализовать last-used metadata

Сохранять lastUsedAt, IP и sanitized user agent.

### 194. Ограничить last-used writes

Не обновлять database на каждый API request.

### 195. Реализовать service accounts

Создавать non-human identities для backend integrations.

### 196. Разделить user и service-account permissions

Не выдавать machine identity интерактивные user capabilities.

### 197. Реализовать API key rate limiting

Применять limits по credential и owner scope.

### 198. Реализовать API key audit

Фиксировать creation, rotation, use, denial и revocation.

### 199. Реализовать secret scanning patterns

Позволить CI и external scanners обнаруживать формат Authgate keys.

### 200. Тестировать API key security

Проверить hashing, scopes, rotation, revocation и prefix collisions.

## 11. OAuth 2.0 authorization server basics

### 201. Спроектировать OAuthClient entity

Хранить clientId, type, redirect URIs, grants, scopes и status.

### 202. Разделить public и confidential clients

Не выдавать client secret приложениям, неспособным его безопасно хранить.

### 203. Реализовать client registration

Создавать OAuth client с валидированными metadata и policies.

### 204. Хранить client secrets как hashes

Показывать raw secret только при создании или rotation.

### 205. Реализовать client secret rotation

Поддерживать controlled overlap нескольких secrets.

### 206. Реализовать redirect URI validation

Требовать точное совпадение зарегистрированного URI.

### 207. Спроектировать AuthorizationCode entity

Хранить code hash, client, user, redirect URI, scopes и expiration.

### 208. Реализовать Authorization Code Flow

Выдавать authorization code после authentication и consent.

### 209. Реализовать PKCE

Поддержать `S256` code challenge для public и confidential clients.

### 210. Запретить implicit flow

Не выдавать access token через browser redirect fragment.

### 211. Реализовать state validation guidance

Документировать обязательное использование state client application.

### 212. Реализовать authorization code one-time use

Атомарно помечать code использованным при token exchange.

### 213. Реализовать token endpoint

Проверять client, grant, code, redirect URI и PKCE verifier.

### 214. Реализовать Client Credentials Flow

Выдавать machine access tokens для service accounts.

### 215. Реализовать refresh token grant

Выполнять rotation и client binding.

### 216. Спроектировать OAuthScope

Хранить стабильный code, description и allowed resource audiences.

### 217. Реализовать scope validation

Не позволять client запрашивать незарегистрированные scopes.

### 218. Реализовать consent screen data

Предоставлять client identity и запрашиваемые permissions.

### 219. Реализовать consent persistence

Сохранять user grants с возможностью отзыва.

### 220. Тестировать OAuth grant flows

Проверить PKCE, redirect URI, code replay, scope escalation и client authentication.

## 12. OpenID Connect и federation basics

### 221. Реализовать OpenID Provider metadata

Создать discovery endpoint с issuer, endpoints и supported algorithms.

### 222. Реализовать ID Token

Выдавать signed token с subject, audience, authTime и nonce.

### 223. Проверять nonce

Связывать authentication request и ID Token для предотвращения replay.

### 224. Реализовать UserInfo endpoint

Возвращать claims в пределах предоставленных scopes.

### 225. Поддержать standard OIDC scopes

Реализовать openid, profile, email и offline_access.

### 226. Реализовать pairwise subject identifiers

Не раскрывать один global user identifier всем clients.

### 227. Реализовать auth_time claim

Позволять clients требовать recent authentication.

### 228. Реализовать max_age

Запрашивать повторную authentication после заданного времени.

### 229. Реализовать prompt behavior

Поддержать login, consent и none semantics.

### 230. Реализовать acr claim

Передавать достигнутый authentication assurance level.

### 231. Реализовать amr claim

Передавать использованные authentication methods.

### 232. Создать external IdP abstraction

Поддержать OIDC identity providers через отдельный adapter.

### 233. Реализовать external OIDC login

Проверять issuer, signature, nonce, state и redirect context.

### 234. Реализовать identity linking

Связывать external subject с internal User через подтверждённый process.

### 235. Запретить unsafe email-based linking

Не объединять accounts только по непроверенному email claim.

### 236. Реализовать external identity unlinking

Не позволять удалить последний доступный authentication method.

### 237. Реализовать JIT user provisioning

Создавать internal identity при первом успешном external login.

### 238. Реализовать external identity audit

Фиксировать linking, login, unlinking и provider errors.

### 239. Создать identity provider simulator

Генерировать valid, expired, replayed и malformed OIDC responses.

### 240. Тестировать federation flows

Проверить account linking, nonce, state, key rotation и provider outage.

## 13. RBAC

### 241. Спроектировать Permission entity

Хранить стабильный code, resource type, action и description.

### 242. Создать permission naming convention

Использовать формат `resource.action`.

### 243. Спроектировать Role entity

Хранить name, type, status, scope и metadata.

### 244. Разделить system и custom roles

Защитить встроенные roles от опасного изменения.

### 245. Спроектировать RolePermission relation

Связывать roles с immutable permission codes.

### 246. Спроектировать RoleAssignment

Связывать subject, role и scope.

### 247. Поддержать global roles

Назначать platform-level administrative permissions.

### 248. Поддержать organization roles

Ограничивать assignment конкретной organization.

### 249. Поддержать project roles

Ограничивать assignment конкретным project.

### 250. Реализовать role hierarchy

Наследовать permissions с защитой от циклов.

### 251. Реализовать custom role creation

Позволить authorized administrators создавать наборы permissions.

### 252. Реализовать role update

Изменять permissions с optimistic locking.

### 253. Реализовать role archive

Запрещать новые assignments без удаления истории.

### 254. Запретить удаление используемой role

Требовать migration assignments.

### 255. Реализовать assignment expiration

Поддержать временные роли.

### 256. Реализовать bulk assignments

Назначать roles нескольким subjects с per-item result.

### 257. Реализовать effective permissions

Вычислять итоговый набор permissions subject в scope.

### 258. Реализовать permission cache

Кэшировать effective permissions с version-based invalidation.

### 259. Реализовать authorization explanation

Показывать, через какую role и assignment предоставлен permission.

### 260. Тестировать RBAC matrix

Проверить roles, scopes, inheritance, expiration и cache invalidation.

## 14. ABAC и policy engine

### 261. Спроектировать SubjectAttributes

Добавить identity type, roles, assurance level и organizational attributes.

### 262. Спроектировать ResourceAttributes

Добавить owner, tenant, classification, status и sensitivity.

### 263. Спроектировать EnvironmentAttributes

Добавить time, IP, network zone, device trust и request channel.

### 264. Создать Policy entity

Хранить effect, actions, resource types, conditions и version.

### 265. Реализовать policy parser

Преобразовывать stored representation в безопасную executable model.

### 266. Запретить dynamic code execution

Не использовать `eval` и произвольный JavaScript для policies.

### 267. Реализовать condition operators

Поддержать equality, membership, comparison, CIDR и time-window checks.

### 268. Реализовать allow policies

Предоставлять access только при совпадении обязательных conditions.

### 269. Реализовать explicit deny

Определить приоритет deny над allow.

### 270. Реализовать default deny

Отклонять request при отсутствии подходящей allow policy.

### 271. Реализовать policy combining algorithm

Зафиксировать deny-overrides или другой deterministic алгоритм.

### 272. Реализовать policy versioning

Сохранять историю изменений authorization rules.

### 273. Реализовать policy activation

Разделить draft, active и archived versions.

### 274. Реализовать policy simulation

Проверять решение без применения новой policy.

### 275. Реализовать policy diff

Показывать изменение effective access.

### 276. Реализовать PolicyDecision

Возвращать effect, matched policies, reason и obligations.

### 277. Реализовать obligations

Требовать MFA, masking или additional audit для разрешённого действия.

### 278. Реализовать policy cache

Кэшировать compiled policies с version key.

### 279. Исследовать OPA и Cedar

Сравнить external policy engines с embedded implementation.

### 280. Тестировать ABAC policies

Проверить attributes, deny precedence, simulation и malformed policies.

## 15. Backend access control patterns

### 281. Создать AuthenticationContext

Передавать subject, session, token, assurance и client metadata.

### 282. Создать AuthorizationContext

Передавать subject, action, resource и environment attributes.

### 283. Реализовать AuthenticationGuard

Проверять supported authentication mechanisms и credential status.

### 284. Реализовать PermissionGuard

Проверять required permissions на controller boundary.

### 285. Реализовать PolicyGuard

Выполнять ABAC evaluation на controller boundary.

### 286. Не ограничивать authorization guards

Повторять критичную проверку внутри application use case.

### 287. Реализовать resource-level authorization

Загружать resource attributes до выполнения mutation.

### 288. Защититься от IDOR

Не считать знание resource identifier доказательством доступа.

### 289. Реализовать ownership policies

Разрешать ограниченные actions владельцу resource.

### 290. Реализовать scope decorators

Объявлять required scopes и permissions без бизнес-логики в metadata.

### 291. Реализовать composite authorization

Объединять permission, ownership, assurance и resource state checks.

### 292. Реализовать field-level authorization

Скрывать чувствительные поля response по policy.

### 293. Реализовать action-level masking

Ограничивать доступные transitions для конкретного subject.

### 294. Реализовать batch authorization

Эффективно проверять список resources без N+1 policy calls.

### 295. Реализовать authorization filtering

Возвращать только resources, доступные caller.

### 296. Не фильтровать полный dataset в memory

Применять authorization scope на query level.

### 297. Реализовать service-to-service authorization

Проверять service identity, audience и machine scopes.

### 298. Реализовать delegated access

Поддержать ограниченное действие от имени пользователя.

### 299. Реализовать impersonation

Сохранять real actor, impersonated subject, scope и expiration.

### 300. Тестировать access control patterns

Проверить guards, use cases, query filtering, field masking и impersonation.

## 16. Rate limiting и abuse prevention

### 301. Определить rate-limit dimensions

Разделить IP, user, session, API key, client и endpoint limits.

### 302. Реализовать fixed-window limiter

Создать базовую реализацию для некритичных endpoints.

### 303. Реализовать sliding-window limiter

Обеспечить более равномерное ограничение requests.

### 304. Реализовать token bucket

Поддержать burst capacity и устойчивую скорость.

### 305. Реализовать Redis-backed limiter

Обеспечить согласованное ограничение между instances.

### 306. Использовать atomic Redis operations

Исключить race conditions при increment и expiration.

### 307. Реализовать login rate limiting

Ограничивать попытки по IP и normalized identity.

### 308. Реализовать distributed password spraying detection

Обнаруживать попытки одного password против множества users.

### 309. Реализовать credential stuffing detection

Обнаруживать массовые attempts с известными credentials.

### 310. Реализовать reset rate limiting

Ограничивать email, IP и device dimensions.

### 311. Реализовать verification resend limits

Предотвращать spam и email abuse.

### 312. Реализовать OAuth endpoint limits

Ограничивать authorization, token и introspection requests.

### 313. Реализовать API key limits

Применять per-key и per-owner quotas.

### 314. Реализовать adaptive throttling

Ужесточать limits при подозрительном risk score.

### 315. Реализовать progressive delay

Увеличивать задержку после повторных authentication failures.

### 316. Избегать permanent account lockout

Не позволять attacker заблокировать чужую identity простыми attempts.

### 317. Реализовать CAPTCHA abstraction

Подключать challenge только для повышенного risk level.

### 318. Реализовать abuse event publishing

Передавать security signals в audit и alerting pipeline.

### 319. Реализовать rate-limit headers

Возвращать limit, remaining и retry time без раскрытия security policy.

### 320. Тестировать abuse controls

Проверить concurrency, distributed limits, bypass attempts и Redis outage.

## 17. Audit logging и security events

### 321. Спроектировать AuditEvent

Хранить actor, action, target, outcome, timestamp и context.

### 322. Разделить audit и application logs

Не использовать обычные logs как authoritative security history.

### 323. Реализовать append-only audit storage

Запретить update и delete через runtime application role.

### 324. Фиксировать authentication events

Сохранять login success, failure, logout и session revocation.

### 325. Фиксировать credential events

Сохранять password change, reset, MFA enrollment и recovery.

### 326. Фиксировать authorization events

Сохранять critical allow и deny decisions.

### 327. Фиксировать role events

Сохранять role creation, permission changes и assignments.

### 328. Фиксировать API key events

Сохранять creation, rotation, use и revocation.

### 329. Фиксировать OAuth events

Сохранять consent, code issuance, token issuance и client failures.

### 330. Фиксировать impersonation events

Сохранять real actor, target identity и performed actions.

### 331. Добавить request context

Хранить requestId, traceId, IP, user agent и clientId.

### 332. Санитизировать audit metadata

Удалять passwords, raw tokens, secrets и sensitive claims.

### 333. Реализовать audit integrity chain

Связывать records hashes для обнаружения изменения истории.

### 334. Реализовать audit retention

Настраивать сроки хранения по event type и compliance requirements.

### 335. Реализовать audit search API

Добавить filtering по actor, action, target, outcome и времени.

### 336. Реализовать audit export

Выгружать records в JSON или CSV с контрольной суммой.

### 337. Реализовать security event severity

Классифицировать informational, warning, high и critical events.

### 338. Реализовать security notifications

Уведомлять пользователя о password reset, new device и API key creation.

### 339. Реализовать alert triggers

Создавать alerts на token reuse, privilege escalation и brute force.

### 340. Тестировать audit completeness

Проверить наличие событий для всех критичных security operations.

## 18. Cryptography, secrets и key management

### 341. Создать cryptographic inventory

Зафиксировать algorithms, keys, purposes, owners и rotation periods.

### 342. Разделить signing и encryption keys

Не использовать один key для разных cryptographic purposes.

### 343. Реализовать key abstraction

Изолировать application code от local files, KMS и HSM.

### 344. Реализовать envelope encryption

Шифровать sensitive values data keys, защищёнными master key.

### 345. Шифровать TOTP secrets

Хранить MFA secrets в encrypted form.

### 346. Шифровать external provider tokens

Защищать refresh tokens и client credentials federation providers.

### 347. Реализовать signing key rotation

Публиковать новые public keys до начала использования private key.

### 348. Реализовать encryption key rotation

Перешифровывать sensitive data без полного downtime.

### 349. Реализовать secret versioning

Хранить key version рядом с encrypted payload.

### 350. Реализовать secret loading

Получать production secrets из защищённого storage.

### 351. Запретить secrets в repository

Добавить secret scanning в pre-commit и CI.

### 352. Запретить secrets в logs

Реализовать centralized redaction.

### 353. Реализовать secure random generation

Использовать operating-system CSPRNG для tokens и keys.

### 354. Реализовать constant-time comparisons

Использовать безопасные comparison functions для signatures и hashes.

### 355. Настроить TLS

Использовать современные protocol versions и certificate validation.

### 356. Реализовать mTLS для internal clients

Аутентифицировать доверенные service-to-service connections.

### 357. Реализовать key compromise procedure

Подготовить emergency rotation и token invalidation.

### 358. Реализовать cryptographic health checks

Проверять наличие active keys без раскрытия secret material.

### 359. Создать cryptographic test vectors

Проверять signing, verification, encryption и rotation.

### 360. Документировать key management lifecycle

Описать generation, distribution, activation, rotation, revocation и destruction.

## 19. Asynchronous workflows и messaging

### 361. Создать integration event envelope

Добавить eventId, type, version, occurredAt, subject и correlationId.

### 362. Разделить domain и integration events

Не публиковать внутренние entities напрямую.

### 363. Реализовать transactional outbox

Атомарно сохранять auth state и integration event.

### 364. Реализовать outbox publisher

Публиковать events через RabbitMQ с confirms и retries.

### 365. Реализовать outbox locking

Использовать `FOR UPDATE SKIP LOCKED`.

### 366. Реализовать outbox cleanup

Архивировать опубликованные records по retention policy.

### 367. Реализовать inbox deduplication

Не обрабатывать integration event повторно.

### 368. Реализовать email jobs

Отправлять verification, reset и security notifications асинхронно.

### 369. Реализовать job idempotency

Не отправлять duplicate email при retry.

### 370. Реализовать delayed jobs

Обрабатывать token cleanup и scheduled session expiration.

### 371. Реализовать retry policy

Повторять transient failures с exponential backoff и jitter.

### 372. Реализовать dead-letter queue

Изолировать необрабатываемые events и jobs.

### 373. Реализовать dead-letter inspection

Показывать event type, subject, attempts и failure reason.

### 374. Реализовать selective redrive

Повторно запускать исправленные jobs с audit trail.

### 375. Реализовать session cleanup job

Удалять или архивировать expired session records.

### 376. Реализовать token cleanup job

Удалять expired verification, reset и refresh token records.

### 377. Реализовать compromised credential notification

Асинхронно уведомлять downstream services о revocation.

### 378. Реализовать authorization cache invalidation events

Инвалидировать permissions после role changes.

### 379. Реализовать event contract versioning

Поддержать backward-compatible evolution.

### 380. Тестировать asynchronous workflows

Проверить retries, duplicate delivery, crash recovery и DLQ.

## 20. Persistence и data model

### 381. Спроектировать PostgreSQL schema

Создать таблицы users, credentials, sessions, tokens, API keys, roles, policies и audit events.

### 382. Использовать database constraints

Закрепить uniqueness, required relations и valid status combinations.

### 383. Добавить unique email index

Использовать normalized email representation.

### 384. Добавить credential constraints

Запретить несколько active password credentials при выбранной модели.

### 385. Добавить session indexes

Оптимизировать поиск по userId, status и expiresAt.

### 386. Добавить refresh token indexes

Оптимизировать поиск по hash, familyId и sessionId.

### 387. Добавить API key prefix index

Ускорить credential lookup.

### 388. Добавить role assignment indexes

Оптимизировать effective-permission queries.

### 389. Добавить audit indexes

Поддержать поиск по actor, target и timestamp.

### 390. Реализовать optimistic locking

Добавить version для User, Role, Policy и OAuthClient.

### 391. Реализовать pessimistic locking

Использовать row locks для token rotation и one-time code consumption.

### 392. Настроить transaction isolation

Выбрать isolation level для credential и authorization operations.

### 393. Реализовать transaction retries

Повторять serialization failures без повторных external side effects.

### 394. Разделить runtime и migration roles

Не предоставлять application permission изменять schema.

### 395. Ограничить database privileges

Предоставить каждому process минимальный набор прав.

### 396. Реализовать soft-delete query policy

Не возвращать deactivated и deleted identities обычным repositories.

### 397. Реализовать data retention jobs

Удалять expired operational records согласно policy.

### 398. Реализовать database backup

Настроить point-in-time recovery.

### 399. Тестировать restore

Восстановить auth database и проверить cryptographic compatibility.

### 400. Документировать data ownership

Зафиксировать authoritative tables и derived cache data.

## 21. Unit и integration testing

### 401. Создать unit tests User state machine

Проверить activation, suspension, lock и deactivation.

### 402. Создать unit tests Email value object

Проверить normalization и invalid formats.

### 403. Создать unit tests password policy

Проверить length, breach detection и history.

### 404. Создать unit tests password hashing

Проверить verification и parameter migration.

### 405. Создать unit tests Session state machine

Проверить expiration, revocation и rotation.

### 406. Создать unit tests RefreshToken family

Проверить rotation, reuse detection и family revocation.

### 407. Создать unit tests API keys

Проверить scopes, expiration и status.

### 408. Создать unit tests OAuth codes

Проверить expiration, PKCE и one-time consumption.

### 409. Создать unit tests RBAC

Проверить roles, hierarchy и scope inheritance.

### 410. Создать unit tests ABAC

Проверить condition operators и deny precedence.

### 411. Создать unit tests rate limiting

Проверить windows, bursts и expiration.

### 412. Создать unit tests audit sanitization

Проверить удаление sensitive fields.

### 413. Создать architecture tests

Проверять layers, modules и запрещённые dependencies.

### 414. Настроить Testcontainers PostgreSQL

Запускать integration tests на реальной database version.

### 415. Настроить Testcontainers Redis

Проверять sessions, rate limits и cache invalidation.

### 416. Настроить Testcontainers RabbitMQ

Проверять outbox, email jobs и security events.

### 417. Создать repository integration tests

Проверить constraints, locks и transaction behavior.

### 418. Создать session integration tests

Проверить cookie, Redis cache и PostgreSQL source of truth.

### 419. Создать token integration tests

Проверить signing, JWKS, rotation и introspection.

### 420. Создать authorization integration tests

Проверить guards, use cases, query filtering и cache invalidation.

## 22. Security testing

### 421. Создать authentication end-to-end tests

Проверить registration, verification, login, refresh и logout.

### 422. Создать password reset end-to-end tests

Проверить request, completion, revocation и notification.

### 423. Создать MFA end-to-end tests

Проверить enrollment, challenge, recovery и step-up.

### 424. Создать API key end-to-end tests

Проверить creation, use, rotation и revocation.

### 425. Создать OAuth Authorization Code tests

Проверить redirect URI, state, PKCE и code replay.

### 426. Создать Client Credentials tests

Проверить client authentication, audience и scopes.

### 427. Создать OIDC tests

Проверить nonce, ID Token, UserInfo и discovery metadata.

### 428. Тестировать user enumeration

Проверить login, registration, reset и verification responses.

### 429. Тестировать session fixation

Проверить rotation identifiers после authentication.

### 430. Тестировать CSRF

Проверить cookie-authenticated mutation endpoints.

### 431. Тестировать token replay

Повторно использовать authorization codes, reset tokens и rotated refresh tokens.

### 432. Тестировать JWT attacks

Проверить algorithm confusion, invalid kid, wrong audience и expired tokens.

### 433. Тестировать IDOR

Использовать identifiers чужих sessions, keys, roles и clients.

### 434. Тестировать privilege escalation

Пытаться назначить себе role или scope без permission.

### 435. Тестировать policy bypass

Проверить missing attributes, malformed conditions и cache staleness.

### 436. Тестировать brute force controls

Проверить distributed login attempts и rate-limit evasion.

### 437. Тестировать race conditions

Параллельно использовать refresh token, reset token и authorization code.

### 438. Тестировать timing differences

Сравнить время ответов для существующих и неизвестных identities.

### 439. Провести dependency security scan

Проверить libraries, container images и transitive dependencies.

### 440. Создать security regression suite

Запускать критичные authentication и authorization tests в CI.

## 23. Performance и reliability

### 441. Определить performance targets

Зафиксировать p95 login, session validation, token issuance и authorization latency.

### 442. Создать login load test

Измерить hashing cost, database load и rate limiting.

### 443. Создать session validation load test

Проверить PostgreSQL и Redis-backed models.

### 444. Создать token issuance load test

Измерить signing throughput и key access overhead.

### 445. Создать JWKS load test

Проверить caching и high-volume resource-server access.

### 446. Создать authorization load test

Измерить RBAC, ABAC и combined policy evaluation.

### 447. Создать API key authentication load test

Измерить prefix lookup и hash verification.

### 448. Создать OAuth token endpoint load test

Проверить code exchange и refresh rotation concurrency.

### 449. Оптимизировать database indexes

Использовать `EXPLAIN ANALYZE` для critical queries.

### 450. Оптимизировать password hashing concurrency

Не блокировать event loop и не исчерпывать worker pool.

### 451. Вынести CPU-bound crypto

Использовать worker threads или controlled native implementation при необходимости.

### 452. Реализовать authorization cache

Кэшировать roles и policies с безопасной invalidation.

### 453. Реализовать JWKS cache

Кэшировать public keys в resource services.

### 454. Реализовать cache stampede protection

Предотвращать массовую одновременную загрузку permissions и keys.

### 455. Реализовать circuit breaker

Изолировать email, external IdP и KMS failures.

### 456. Реализовать timeout policy

Ограничить database, Redis, provider и KMS calls.

### 457. Реализовать graceful degradation

Сохранять local authentication при недоступности необязательных providers.

### 458. Провести soak test

Обнаружить memory leaks, session growth и connection leaks.

### 459. Провести dependency outage tests

Отключать Redis, RabbitMQ, email provider и external IdP.

### 460. Создать capacity model

Рассчитать instances, database, Redis и cryptographic throughput.

## 24. Observability

### 461. Реализовать structured logging

Добавить service, environment, requestId, traceId, userId и sessionId.

### 462. Псевдонимизировать identity data

Не записывать raw email и tokens в logs.

### 463. Реализовать centralized redaction

Удалять passwords, cookies, authorization headers и secrets.

### 464. Реализовать OpenTelemetry tracing

Трассировать HTTP, database, Redis, messaging и external providers.

### 465. Добавить authentication spans

Измерять lookup, password verification, MFA и session creation.

### 466. Добавить authorization spans

Измерять policy evaluation и cache operations.

### 467. Добавить token spans

Измерять signing, verification, introspection и rotation.

### 468. Добавить authentication metrics

Собирать successes, failures, lockouts и MFA challenges.

### 469. Добавить session metrics

Собирать active, created, revoked и expired sessions.

### 470. Добавить token metrics

Собирать issued, refreshed, reused и revoked tokens.

### 471. Добавить API key metrics

Собирать authentications, failures, expirations и revocations.

### 472. Добавить OAuth metrics

Собирать authorization, token grants, failures и consent events.

### 473. Добавить authorization metrics

Собирать allow, deny, evaluation duration и cache hit rate.

### 474. Добавить rate-limit metrics

Собирать blocked requests по endpoint и credential type.

### 475. Добавить audit metrics

Собирать ingestion rate, export failures и integrity errors.

### 476. Создать Grafana authentication dashboard

Показать login rates, failures, MFA и sessions.

### 477. Создать Grafana authorization dashboard

Показать decisions, latency и cache performance.

### 478. Создать Grafana security dashboard

Показать brute force, token reuse и privilege escalation events.

### 479. Настроить alerts

Создать alerts на login failure spikes, token reuse и signing-key failures.

### 480. Определить Authgate SLI и SLO

Зафиксировать availability, authentication latency и authorization correctness indicators.

## 25. Deployment и эксплуатация

### 481. Создать production Dockerfiles

Использовать multi-stage build, non-root user и minimal runtime image.

### 482. Разделить API и worker deployments

Масштабировать synchronous и asynchronous workloads независимо.

### 483. Настроить resource limits

Ограничить CPU и memory для API и workers.

### 484. Настроить rolling deployments

Сохранять sessions и token validation во время обновления instances.

### 485. Реализовать graceful draining

Завершать active authentication requests перед shutdown.

### 486. Создать migration policy

Использовать expand-migrate-contract для backward-compatible schema changes.

### 487. Реализовать zero-downtime key rotation

Обновлять signing keys без отказа verification.

### 488. Реализовать zero-downtime cookie changes

Поддерживать переход между cookie names и secrets.

### 489. Настроить autoscaling

Масштабировать API по latency, CPU и request rate.

### 490. Ограничить autoscaling

Не перегружать PostgreSQL, Redis и KMS.

### 491. Настроить PostgreSQL backup

Обеспечить point-in-time recovery.

### 492. Настроить Redis persistence policy

Определить recovery requirements для sessions и rate limits.

### 493. Создать disaster recovery plan

Описать восстановление database, keys, sessions и OAuth clients.

### 494. Провести disaster recovery test

Восстановить environment и проверить token verification.

### 495. Создать runbook login failure spike

Описать диагностику credentials, dependencies и attack traffic.

### 496. Создать runbook token reuse incident

Описать revocation, user notification и forensic analysis.

### 497. Создать runbook signing-key compromise

Описать emergency rotation и mass token invalidation.

### 498. Создать runbook external IdP outage

Описать fallback и communication procedures.

### 499. Создать runbook Redis outage

Описать session validation и rate-limit fallback.

### 500. Создать runbook authorization incident

Описать containment, policy rollback и audit investigation.

## 26. Документация и production-style сценарии

### 501. Создать README репозитория

Описать назначение Authgate, architecture, запуск и основные flows.

### 502. Создать C4 System Context diagram

Показать users, clients, resource services и external identity providers.

### 503. Создать C4 Container diagram

Показать Auth API, workers, PostgreSQL, Redis, broker и KMS.

### 504. Создать component diagrams

Показать Identity, Sessions, Tokens, OAuth, Authorization и Audit modules.

### 505. Создать sequence diagram password login

Показать credential verification, MFA, session и token issuance.

### 506. Создать sequence diagram refresh rotation

Показать token family, reuse detection и revocation.

### 507. Создать sequence diagram OAuth flow

Показать authorization, consent, PKCE и token exchange.

### 508. Создать sequence diagram API key authentication

Показать prefix lookup, hash verification, scopes и audit.

### 509. Создать sequence diagram authorization

Показать context building, RBAC, ABAC и decision enforcement.

### 510. Документировать authentication state machines

Описать User, Session, RefreshToken и MFA states.

### 511. Документировать authorization model

Описать roles, permissions, scopes, policies и decision precedence.

### 512. Документировать token model

Описать claims, lifetime, rotation, introspection и revocation.

### 513. Создать ADR session strategy

Обосновать server-side sessions, JWT или hybrid model.

### 514. Создать ADR password hashing

Зафиксировать algorithm, parameters и upgrade strategy.

### 515. Создать ADR authorization architecture

Обосновать RBAC, ABAC и policy engine boundaries.

### 516. Реализовать production-style browser authentication

Показать registration, verification, login, MFA, cookie session и logout.

### 517. Реализовать production-style token flow

Показать access token, refresh rotation, reuse attack и family revocation.

### 518. Реализовать production-style machine access

Показать service account, API key, OAuth Client Credentials и scoped authorization.

### 519. Реализовать production-style security incident

Сымитировать credential compromise, revoke credentials и восстановить access.

### 520. Подготовить production readiness checklist

Зафиксировать обязательные проверки authentication, authorization, cryptography, observability, recovery и operations.
