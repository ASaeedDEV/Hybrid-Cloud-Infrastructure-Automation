# Hybrid-Cloud-Infrastructure-Automation

This project is a minimalist cloud instance manager written in Go. It allows you to securely and efficiently create, list, start, stop, and terminate cloud instances. The goal is to provide a simple and user-friendly tool for managing Amazon Web Services (AWS) instances.

## Features

- Create cloud instances with a single API call
- List cloud instances in a specified region
- Start, stop, and terminate instances safely
- DryRun mode to test code without modifying actual AWS resources
- Support for low-cost instances (e.g., t2.micro)
- Support for multiple instance types (e.g., t2.micro, t2.small, etc.)

## Requirements

- Go version 1.17 or higher
- AWS SDK for Go
- AWS credentials with limited permissions
- A valid AWS account

## Setup

### 1. AWS Credentials

Make sure your AWS credentials are configured on your machine. Run:

```sh
aws configure
```

You’ll be prompted for your `AWS Access Key ID`, `AWS Secret Access Key`, default region, and output format. If already set, you can skip this step.

### 2. Region Configuration

Set your preferred AWS region using an environment variable. If omitted, `us-west-2` will be used by default:

```sh
export AWS_REGION=your-region
```

### 3. Enable DryRun Mode

To test functionality without creating/modifying AWS resources:

```sh
export DRY_RUN=true
```

## Installation

1. Clone the repository:

   ```sh
   git clone https://github.com/elliotsecops/Cloud-Instance-Manager.git
   ```

2. Navigate to the project directory:

   ```sh
   cd Cloud-Instance-Manager
   ```

3. Install dependencies:

   ```sh
   go get -u github.com/aws/aws-sdk-go-v2/aws
   ```

## Usage

### Running the Program

Run the main program using:

```sh
go run main.go
```

### Example Commands

#### Create an Instance

Creates a cloud instance with default AMI `ami-12345678`. You can modify the AMI in the code:

```go
instanceID, err := crearInstancia("ami-12345678")
if err != nil {
    log.Fatalf("Error creating instance: %v", err)
}
fmt.Printf("Instance created: %s\n", instanceID)
```

#### List Instances

Lists all instances in the configured region:

```go
instances, err := listarInstancias()
if err != nil {
    log.Fatalf("Error listing instances: %v", err)
}
for _, instance := range instances {
    fmt.Printf("ID: %s, State: %s\n", *instance.InstanceId, instance.State.Name)
}
```

#### Start an Instance

Starts the specified instance:

```go
if err := iniciarInstancia(instanceID); err != nil {
    log.Fatalf("Error starting instance: %v", err)
}
fmt.Println("Instance started")
```

#### Stop an Instance

Stops the specified instance:

```go
if err := detenerInstancia(instanceID); err != nil {
    log.Fatalf("Error stopping instance: %v", err)
}
fmt.Println("Instance stopped")
```

#### Terminate an Instance

Terminates the specified instance:

```go
if err := terminarInstancia(instanceID); err != nil {
    log.Fatalf("Error terminating instance: %v", err)
}
fmt.Println("Instance terminated")
```

## Testing

### DryRun Testing

To simulate actions without making changes to AWS:

```sh
export DRY_RUN=true
go run main.go
```

### Unit Tests

Run unit tests with:

```sh
go test -v
```

### Integration Tests

Run integration tests with:

```sh
go test -v -tags=integration
```

## License

This project is licensed under the MIT License, allowing you to freely use, modify, and distribute the code as long as the original license terms are followed.

## Contributing

To contribute:

1. Clone the repo:

   ```sh
   git clone https://github.com/elliotsecops/Cloud-Instance-Manager.git
   ```

2. Create a new branch:

   ```sh
   git branch my-branch
   ```

3. Make your changes

4. Submit a pull request

## Reporting Issues

If you encounter bugs or issues, please open an issue on the GitHub repo to help improve the project.

---

Let me know if you'd like this formatted into a `README.md` file.
