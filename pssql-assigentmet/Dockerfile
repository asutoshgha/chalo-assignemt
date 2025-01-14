 Use the official Python image
FROM python:3.9-slim

# Set the working directory in the container
WORKDIR /app

# Copy the current directory contents into the container
COPY . /app

# Install required dependencies, Ansible, Terraform, and SSH
RUN apt-get update && apt-get install -y --no-install-recommends \
    wget \
    curl \
    gnupg \
    sshpass \
    openssh-client \
    python3 \
    python3-pip \
    unzip \
    && pip install ansible flask \
    && wget -q https://releases.hashicorp.com/terraform/1.5.0/terraform_1.5.0_linux_amd64.zip \
    && unzip terraform_1.5.0_linux_amd64.zip -d /usr/local/bin/ \
    && rm terraform_1.5.0_linux_amd64.zip \
    && ssh-keygen -t rsa -b 2048 -f /root/.ssh/id_rsa -q -N "" \
    && apt-get remove -y wget curl gnupg unzip \
    && apt-get autoremove -y \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*


# Expose the application port
EXPOSE 5000

# Command to run the application
CMD ["python", "app.py"]
