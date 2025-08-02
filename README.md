# AWS S3 Bucket with Versioning and Encryption (Terraform Project)

This project demonstrates how to provision an S3 bucket using Terraform with:
- **Versioning** enabled to keep multiple versions of an object.
- **AES-256 encryption** enabled for server-side encryption.

## Files
- `main.tf`: Main Terraform configuration file.
- `provider.tf`: A Terraform configuration file that defines the cloud or infrastructure provider (e.g., AWS, Azure, Google Cloud) and its settings. It specifies the provider's API endpoint, credentials, and other configuration options.
- `variable.tf`: A Terraform configuration file that defines input variables for your infrastructure deployment. These variables can be used to customize the deployment, such as specifying instance types, regions, or other settings. Variables can be assigned values when running Terraform.
- `outputs.tf`: A Terraform configuration file that defines output values from your infrastructure deployment. These outputs can be used to display important information, such as IP addresses, instance IDs, or DNS names, after the deployment is complete. Outputs can be useful for automation or integration with other tools.

## Steps to Run

1. **Initialize Terraform:**
   ```bash
   terraform init
   ```

2. **Preview the changes Terraform will make:**
   ```bash
   terraform plan
   ```

3. **Apply the configuration:**
   ```bash
   terraform apply
   ```

4. **To destroy the resources when done:**
   ```bash
   terraform destroy
   ```

## Notes
- Be sure to configure your AWS credentials (`aws configure` or environment variables).
- The S3 bucket name must be globally unique. You may need to change `my-versioned-encrypted-bucket-001`.

## License
MIT License
