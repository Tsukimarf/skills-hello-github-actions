# Upgrade Guide

This document provides detailed instructions for upgrading between major versions of this project.

## Table of Contents

- [General Upgrade Process](#general-upgrade-process)
- [Version-Specific Guides](#version-specific-guides)
  - [Upgrading to v2.x](#upgrading-to-v2x)
  - [Upgrading to v1.5](#upgrading-to-v15)
  - [Upgrading from v1.0 to v1.4](#upgrading-from-v10-to-v14)
- [Breaking Changes](#breaking-changes)
- [Deprecation Notices](#deprecation-notices)
- [Migration Tools](#migration-tools)
- [Rollback Procedures](#rollback-procedures)
- [Getting Help](#getting-help)

---

## General Upgrade Process

Before upgrading to any new version, follow these steps:

### 1. Pre-Upgrade Checklist

- [ ] **Backup your data** and configuration files
- [ ] **Review the changelog** for the target version
- [ ] **Check system requirements** for the new version
- [ ] **Test in a non-production environment** first
- [ ] **Update dependencies** to compatible versions
- [ ] **Read breaking changes** documentation carefully
- [ ] **Plan downtime** if required
- [ ] **Notify stakeholders** of the upgrade schedule

### 2. Recommended Upgrade Path

Always upgrade incrementally rather than skipping major versions:

```
v1.0 → v1.5 → v2.0 → latest
```

**Example**: To upgrade from v1.2 to v2.1:
1. First upgrade to v1.5
2. Then upgrade to v2.0
3. Finally upgrade to v2.1

### 3. Standard Upgrade Steps

```bash
# 1. Backup current installation
cp -r /path/to/project /path/to/project.backup

# 2. Stop the application
./stop.sh  # or your stop command

# 3. Update to new version
git fetch --tags
git checkout v2.0.0  # or your target version

# 4. Install dependencies
npm install  # or pip install -r requirements.txt, etc.

# 5. Run migrations (if applicable)
./migrate.sh  # or your migration command

# 6. Update configuration
# Review and update config files as needed

# 7. Start the application
./start.sh  # or your start command

# 8. Verify the upgrade
./health-check.sh  # or test key functionality
```

---

## Version-Specific Guides

## Upgrading to v2.x

**Release Date**: January 2025  
**Status**: Latest stable release  
**Difficulty**: ⚠️ Moderate (Breaking changes)

### New Features
- Enhanced security features
- Performance improvements (30% faster)
- Modern API design
- Improved error handling
- Better logging and monitoring

### Breaking Changes

#### 1. Configuration Format Change

**Old format (v1.x):**
```yaml
# config.yml
database:
  host: localhost
  port: 5432
  name: mydb
```

**New format (v2.x):**
```yaml
# config.yml
database:
  connection:
    host: localhost
    port: 5432
  database_name: mydb
  pool_size: 10
```

**Migration**: Run the configuration migration tool:
```bash
./tools/migrate-config.sh config.yml
```

#### 2. API Endpoint Changes

| Old Endpoint (v1.x) | New Endpoint (v2.x) | Notes |
|---------------------|---------------------|-------|
| `/api/user` | `/api/v2/users` | Pluralized, versioned |
| `/api/auth/login` | `/api/v2/auth/login` | Versioned only |
| `/api/data` | `/api/v2/resources` | Renamed for clarity |

**Migration**: Update all API calls to use `/api/v2/` prefix.

#### 3. Removed Dependencies

The following dependencies have been removed:
- `old-library` - Replace with `new-library`
- `deprecated-module` - Functionality built-in now

**Migration**:
```bash
npm uninstall old-library
npm install new-library
```

Update imports:
```javascript
// Old
import { feature } from 'old-library';

// New
import { feature } from 'new-library';
```

#### 4. Method Signature Changes

```python
# Old (v1.x)
def process_data(data):
    return result

# New (v2.x)
def process_data(data, options=None):
    return result
```

### Database Migrations

Run the following migrations in order:

```bash
# 1. Backup database
pg_dump mydb > backup_v1.sql

# 2. Run migrations
python manage.py migrate --from v1.5 --to v2.0

# 3. Verify data integrity
python manage.py check-integrity
```

### Environment Variables

New required environment variables:

```bash
# Add to .env file
API_VERSION=v2
FEATURE_FLAG_NEW_AUTH=true
LOG_LEVEL=info
CACHE_ENABLED=true
```

### Performance Considerations

- **Memory**: v2.x requires 20% more memory
- **Disk Space**: Additional 500MB for new features
- **CPU**: Better multi-threading support

### Step-by-Step Upgrade

```bash
# 1. Backup everything
./backup.sh --full

# 2. Stop services
systemctl stop myapp

# 3. Checkout v2.0
git checkout v2.0.0

# 4. Install dependencies
npm install

# 5. Migrate configuration
./tools/migrate-config.sh

# 6. Migrate database
npm run migrate

# 7. Update environment variables
cp .env.example .env
# Edit .env with your values

# 8. Start services
systemctl start myapp

# 9. Health check
curl http://localhost:8080/health

# 10. Verify functionality
npm test
```

---

## Upgrading to v1.5

**Release Date**: March 2024  
**Status**: LTS (Long-term Support)  
**Difficulty**: ✅ Easy (Minor breaking changes)

### What's New
- Security patches
- Bug fixes
- Minor feature additions
- Improved documentation

### Breaking Changes

#### Deprecated Function Renamed

```javascript
// Old (v1.4 and earlier)
calculateTotal(items)

// New (v1.5+)
computeTotal(items)
```

**Migration**: Simple find-and-replace in your codebase.

### Upgrade Steps

```bash
# 1. Backup
cp -r project project.backup

# 2. Update
git checkout v1.5.0
npm install

# 3. Update deprecated functions
# Use your IDE's find-and-replace

# 4. Test
npm test

# 5. Deploy
npm run deploy
```

---

## Upgrading from v1.0 to v1.4

**Difficulty**: ✅ Easy (No breaking changes)

These are patch releases with bug fixes and minor improvements.

```bash
# Simple update process
git checkout v1.4.0
npm install
npm test
```

---

## Breaking Changes

### Complete Breaking Changes List

#### v2.0.0
- Configuration file format changed
- API endpoints versioned with `/api/v2/`
- Minimum Node.js version: 18.x (was 16.x)
- PostgreSQL 13+ required (was 11+)
- Removed support for legacy authentication

#### v1.5.0
- Function `calculateTotal()` renamed to `computeTotal()`
- Minimum Python version: 3.9+ (was 3.7+)

---

## Deprecation Notices

### Currently Deprecated (Will be removed in v3.0)

| Feature | Deprecated In | Removal In | Replacement |
|---------|--------------|------------|-------------|
| `oldMethod()` | v2.0 | v3.0 | `newMethod()` |
| Legacy config format | v2.0 | v3.0 | New YAML format |
| `/api/v1/` endpoints | v2.0 | v3.0 | `/api/v2/` endpoints |

### How to Prepare

```bash
# Check for deprecated features in your code
./tools/check-deprecated.sh

# View deprecation warnings
npm run lint -- --show-deprecated
```

---

## Migration Tools

We provide several tools to help with upgrades:

### Configuration Migrator

```bash
# Migrate config from v1.x to v2.x
./tools/migrate-config.sh old-config.yml new-config.yml

# With validation
./tools/migrate-config.sh old-config.yml new-config.yml --validate
```

### Database Migrator

```bash
# Dry run (preview changes)
./tools/migrate-db.sh --dry-run

# Actual migration
./tools/migrate-db.sh --from v1.5 --to v2.0

# Rollback if needed
./tools/migrate-db.sh --rollback
```

### Code Scanner

```bash
# Scan for deprecated code patterns
./tools/scan-deprecated.sh /path/to/your/code

# Auto-fix simple issues
./tools/scan-deprecated.sh /path/to/your/code --auto-fix
```

---

## Rollback Procedures

If you encounter issues after upgrading:

### Quick Rollback

```bash
# 1. Stop application
./stop.sh

# 2. Restore from backup
rm -rf /path/to/project
cp -r /path/to/project.backup /path/to/project

# 3. Restore database (if needed)
psql mydb < backup.sql

# 4. Start application
./start.sh
```

### Detailed Rollback Steps

1. **Document the issue**
   ```bash
   ./logs/capture-error.sh > rollback-reason.log
   ```

2. **Stop all services**
   ```bash
   systemctl stop myapp
   systemctl stop myapp-worker
   ```

3. **Restore application files**
   ```bash
   git checkout v1.5.0  # previous version
   npm install
   ```

4. **Restore database**
   ```bash
   # PostgreSQL
   dropdb mydb
   createdb mydb
   psql mydb < backup_pre_upgrade.sql
   
   # MySQL
   mysql -u root -p mydb < backup_pre_upgrade.sql
   ```

5. **Verify rollback**
   ```bash
   ./health-check.sh
   npm test
   ```

6. **Restart services**
   ```bash
   systemctl start myapp
   systemctl start myapp-worker
   ```

---

## System Requirements

### v2.x Requirements

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| Node.js | 18.x | 20.x LTS |
| PostgreSQL | 13 | 15+ |
| RAM | 2GB | 4GB+ |
| Disk Space | 1GB | 5GB+ |
| OS | Ubuntu 20.04+ | Ubuntu 22.04+ |

### v1.5 Requirements

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| Node.js | 16.x | 18.x |
| PostgreSQL | 11 | 13+ |
| RAM | 1GB | 2GB+ |
| Disk Space | 500MB | 2GB+ |

---

## Testing Your Upgrade

### Pre-Upgrade Tests

```bash
# Run full test suite
npm test

# Run integration tests
npm run test:integration

# Check for known issues
./tools/pre-upgrade-check.sh
```

### Post-Upgrade Tests

```bash
# Verify installation
npm run verify

# Smoke tests
npm run test:smoke

# Performance tests
npm run test:performance

# Health check
curl http://localhost:8080/health
```

---

## Getting Help

### Before Upgrading

- Review [CHANGELOG.md](./CHANGELOG.md) for detailed changes
- Check [GitHub Discussions](https://github.com/yourorg/project/discussions) for upgrade experiences
- Read [Migration FAQ](./docs/MIGRATION_FAQ.md)

### During/After Upgrade

- **Issues**: [GitHub Issues](https://github.com/yourorg/project/issues)
- **Discussions**: [Community Forum](https://github.com/yourorg/project/discussions)
- **Chat**: [Discord Server](https://discord.gg/yourproject)
- **Email**: support@yourproject.com

### Emergency Support

For critical production issues:
- **Enterprise Support**: support@yourproject.com (24/7)
- **Community Slack**: #urgent-help channel
- **Phone**: +1-XXX-XXX-XXXX (Enterprise customers only)

---

## Additional Resources

- [Full Changelog](./CHANGELOG.md)
- [API Documentation](https://docs.yourproject.com)
- [Migration FAQ](./docs/MIGRATION_FAQ.md)
- [Video Tutorial: Upgrading to v2.0](https://youtube.com/watch?v=...)
- [Blog Post: What's New in v2.0](https://blog.yourproject.com/v2-release)

---

**Last Updated**: January 2025  
**Document Version**: 2.0

For questions about this upgrade guide, please [open an issue](https://github.com/yourorg/project/issues).