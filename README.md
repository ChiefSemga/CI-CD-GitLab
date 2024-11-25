# CI-CD-GitLab

# Project: To create a pseudo Gitlab CI pipeline (deliver a .yaml file), with the following stages:


- Build

- Static code analysis

- Test

- Deployment

 

1. The build consists of 3 different platforms (PowerPC, imx8, Linux-x) that needs to be build in its own build stage. Each platform uses a different toolchain image

2. All platform needs to be tested in its own test stage, depending on the corresponding build stage

3. Test should also include static analysis in its own stages

4. Deploy stages downloads the build software to a target and verify that the download is successful by executing a smoke test on each platform

5. For the build stages please define a reusable stage template

6. For the static code analysis, please utilize an external repo with shared Gitlab CI templates

7. Static code analysis takes an argument based on the platform

8. All builds are build during development, but imx8 is the only platform build on release rules from main and tagged


# Step by step Explanation
# GitLab CI/CD Pipeline for Multi-Platform Build, Test, and Deployment
This project demonstrates a complete GitLab CI/CD pipeline designed to build, test, and deploy software for three different platforms: 
PowerPC,
imx8, and 
Linux-x. 
Each platform has its own specific toolchain, static analysis requirements, and deployment processes.

The pipeline is configured in the .gitlab-ci.yml file, with clear separation into the following stages:

Build
Static Code Analysis
Test
Deployment
This README provides an overview of the pipeline, its structure, and how to use it effectively.
# Pipeline Overview
# Stages and Jobs

# 1. Build Stage

# Purpose: 
Compile the source code for the target platform using platform-specific toolchains.
# Platforms: 
PowerPC, imx8, Linux-x.
# Key Features:
Uses a reusable job template (.build_template) for consistent configuration.
Executes platform-specific builds with individual Makefiles (Makefile.powerpc, Makefile.imx8, Makefile.linux-x).
Builds on different branches:
imx8 is only built on main or tagged releases.
PowerPC and Linux-x are built on the development branch and tagged releases.
# 2. Static Code Analysis Stage
# Purpose:
Perform static code analysis to ensure code quality and detect potential issues.
# Key Features:
Uses an external GitLab CI template repository for static analysis scripts.
Each platform runs static analysis with platform-specific configurations (e.g., --platform argument).
Supports static analysis for all branches and tagged releases.
# 3. Test Stage
# Purpose:
Execute unit and integration tests on the built artifacts.
# Key Features:
Each platform has its own test job with platform-specific Makefiles.
Ensures that tests run only after the successful completion of the respective build stage.
# 4. Deployment Stage
# Purpose:
Deploy the built software to a target server and verify deployment with a smoke test.
# Key Features:
Artifacts are uploaded to the target server using scp.
Smoke tests are performed via SSH to ensure successful deployment.
