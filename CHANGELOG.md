# Changelog

## 2.1.2 - 2026-10-20 (fork: Sylph/catlink)

### Security
- `api_url()` now requires https and an official `catlinks.cn` API host (or the
  explicitly configured base host). This closes a credential-exfiltration path:
  the `request_api` entity service previously accepted any absolute URL and
  would send the session token to it.
- `Account.request()` no longer mutates the caller's params dict; the injected
  `token`/`sign` values were leaking into every device action log that printed
  its params.
- Failed-login, request-failure and API-response logs no longer dump credentials,
  tokens, request params or full response bodies.
- Removed the unused `RSA_PRIVATE_KEY` constant committed in `const.py`.
- README: removed `wget | bash` install methods (remote code execution).

### Fixed
- Unhandled `NoneType` exceptions when the API returns present-but-null
  `deodorantCountdown`, `catLitterWeight`, `inductionTimes` or `manualTimes`
  (log spam every poll cycle; thanks to meeowgler for the upstream PR #67 base).
- Device-log polling no longer logs a warning every cycle when a device simply
  has no recent activity (empty list with returnCode 0).
- Entities now register with their platform domain (`sensor.`, `select.`, ...)
  instead of `catlink.` (upstream issue #61; HA removes support for the wrong
  domain in 2027.5).
- `test_platforms_loaded` assertion updated to include the `number` domain.

## 2.1.1 - 2026-02-06

### Added
- Open-X/C08 device support (thanks to this nice repo: https://github.com/eulemitkeule/pycatlink)
- Limited Scooper Pro Ultra support
- Reset litter and reset deodorant buttons for litterbox
- Config flow coverage for discovery, reauthentication, and options
- Test suite additions and GitHub Actions workflow for tests

### Fixed
- Device detail parsing fallback when API payloads are incomplete
- Home Assistant 2026.2.0 compatibility issues

### Changed
- Device and entity organization with new helpers and logs mixin
