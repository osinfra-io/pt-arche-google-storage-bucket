# Google Cloud Platform - Storage Bucket OpenTofu Module

[![OpenTofu Tests](https://img.shields.io/github/actions/workflow/status/osinfra-io/pt-arche-google-storage-bucket/test.yml?style=for-the-badge&logo=opentofu&color=FEDA15&label=OpenTofu%20Tests)](https://github.com/osinfra-io/pt-arche-google-storage-bucket/actions/workflows/test.yml) [![Dependabot](https://img.shields.io/github/actions/workflow/status/osinfra-io/pt-arche-google-storage-bucket/dependabot.yml?style=for-the-badge&logo=github&color=2088FF&label=Dependabot)](https://github.com/osinfra-io/pt-arche-google-storage-bucket/actions/workflows/dependabot.yml) [![Datadog Security Enabled](https://img.shields.io/badge/Datadog%20Security-Enabled-632CA6?style=for-the-badge&logo=datadog)](https://app.datadoghq.com/security/code-security/repositories?repository_id=pt-arche-google-storage-bucket)

## Repository Description

Reusable OpenTofu child module that creates a Google Cloud Storage bucket with uniform bucket-level access enforced, public access prevention, and optional object versioning. It supports customer-managed encryption keys (CMEK) and a configurable storage class (STANDARD, NEARLINE, COLDLINE, ARCHIVE, etc.).

## 🔩 Usage

### Module interface

Consume the repository root with `source = "github.com/osinfra-io/pt-arche-google-storage-bucket?ref=<commit_sha>"`. See [`variables.tofu`](variables.tofu) and [`outputs.tofu`](outputs.tofu).

Uniform bucket-level access and public access prevention are enforced by default, object versioning defaults to enabled, and `force_destroy` defaults to false. An optional CMEK can be supplied through `default_kms_key_name`; the caller must grant the Cloud Storage service agent access to that key. Versioning, retained noncurrent objects, non-Standard storage classes, data retrieval, egress, and KMS operations can increase cost. Setting `force_destroy = true` permits deletion of all objects with the bucket and should be used only when that data-loss behavior is intentional.

> [!TIP]
> You can check the [tests/fixtures](tests/fixtures) directory for example configurations. These fixtures set up the system for testing by providing all the necessary initial code, thus creating good examples on which to base your configurations.

Google project services must be enabled before using this module. As a best practice, these should be defined in the [pt-arche-google-project](https://github.com/osinfra-io/pt-arche-google-project) module. The following services are required:

- `storage.googleapis.com`

## 🛠️ Tools

- [osinfra-pre-commit-hooks](https://github.com/osinfra-io/pt-techne-pre-commit-hooks)
- [pre-commit](https://github.com/pre-commit/pre-commit)

## 📋 Skills and Knowledge

- [storage bucket](https://cloud.google.com/storage/docs/buckets)

## 🔍 Tests

Tests use [mocked providers](https://opentofu.org/docs/cli/commands/test/#the-mock_provider-blocks); no infrastructure or credentials are required.

```none
tofu init
```

```none
tofu test
```

## 📦 Release

To release a new version, simply push a new tag to the repository. The tag should be in the format `vX.Y.Z` where `X`, `Y`, and `Z` are integers.

```none
git tag vX.Y.Z
git push origin vX.Y.Z
```
