---
title: "Importing a project by git URL"
id: "cloud-import-a-project-by-git-url"
---

In dbt Cloud. You can import a git repository from any valid git URL that points to a dbt project. There are a couple of important considerations to keep in mind when doing this:

## Git protocols
You must use the `git@...` or `ssh:..`. version of your git URL, not the `https://...` version. dbt Cloud uses the SSH protocol to clone repositories, so dbt Cloud will be unable to clone repos supplied with the HTTP protocol.

## Managing Deploy Keys
After importing a project by Git URL, dbt Cloud will generate a Deploy Key for your repository. You must provide this Deploy Key in the Repository configuration of your Git host. This Deploy Key should be be configured to allow *read and write access* to the specified repositories.

### GitHub

:::info Use GitHub?

If you use GitHub, you can import your repo directly using [dbt Cloud's GitHub Application](cloud-installing-the-github-application). Connecting your repo via the GitHub Application [enables Continuous Integration](cloud-enabling-continuous-integration-with-github) for scheduled dbt runs.

:::

To add a deploy key to a GitHub account, navigate to the Deploy keys tab of the settings page in your GitHub repository. After supplying a name for the deploy key and pasting in your deploy key (generated by dbt Cloud), be sure to check the "Allow write access" checkbox. After adding this key, dbt Cloud will be able to read and write files in your dbt project.

See also:  [Adding a deploy key in GitHub](https://github.blog/2015-06-16-read-only-deploy-keys/)

<Lightbox src="/img/docs/dbt-cloud/cloud-configuring-dbt-cloud/cd7351c-Screen_Shot_2019-10-16_at_1.09.41_PM.png" title="Configuring a GitHub Deploy Key"/>

### BitBucket

To add a deploy key to a BitBucket account, navigate to "SSH keys" tab in the Personal Settings page of your BitBucket account. Next, click the "Add key" button and paste in the deploy key generated by dbt Cloud for your repository. After saving this SSH key, dbt Cloud will be able to read and write files in your BitBucket repository.

<Lightbox src="/img/docs/dbt-cloud/cloud-configuring-dbt-cloud/bitbucket-ssh-key.png" title="Configuring a BitBucket SSH Key"/>

### GitLab

To add a deploy key to a GitLab account, navigate to the [SSH keys](https://gitlab.com/profile/keys) tab in the User Settings page of your GitLab account. Next, paste in the deploy key generated by dbt Cloud for your repository. After saving this SSH key, dbt Cloud will be able to read and write files in your GitLab repository.

See also:  [Adding a read only deploy key in GitLab](https://docs.gitlab.com/ee/ssh/#per-repository-deploy-keys)

<Lightbox src="/img/docs/dbt-cloud/cloud-configuring-dbt-cloud/f3ea88d-Screen_Shot_2019-10-16_at_4.45.50_PM.png" title="Configuring a GitLab SSH Key"/>

### AWS CodeCommit

dbt Cloud can work with dbt projects hosted on AWS CodeCommit, but there are some extra steps needed compared to Github or other git providers. This guide will help you connect your CodeCommit-hosted dbt project to dbt Cloud.

#### Step 1: Create an AWS User for dbt Cloud

To give dbt Cloud access to your repository, first you'll need to create an AWS IAM user for dbt Cloud. Log into the AWS Console and navigate to the IAM section. Click "Add User", and create a new user with "Programmatic Access".

This user will need clone access to your repository. The easiest way to set that up is to add the "AWSCodeCommitReadOnly" permission during setup.

#### Step 2: Import your repository by name

Open the AWS CodeCommit console and choose your repository. Copy the SSH URL from that page. Next, navigate to the "New Repository" page in dbt Cloud. Choose the "Git URL" tab, and paste in the SSH URL you copied from the console.

In the newly created Repository details page, you'll see a "Deploy Key" field. Copy the contents of this field as you'll need it for step 3.

#### Step 3: Grant dbt Cloud AWS User access

Open up the newly created dbt Cloud user in the AWS IAM Console. Choose the "Security Credentials" tab and then click "Upload SSH public key". Paste in the contents of the "Public Key" field from the dbt Cloud Repository page.

Once you've created the key, you'll see an "SSH key ID" for it. You'll need to write into support and share that field so that dbt Cloud support can complete the setup process for you.

You're all set! Once support handles your request, your project is set up and you can begin executing dbt runs from dbt Cloud.

### Azure DevOps

To add a deploy key to an Azure DevOps account, navigate to the "SSH public keys" page in the User Settings of your Azure DevOps account.

<Lightbox src="/img/docs/dbt-cloud/cloud-configuring-dbt-cloud/52bfdaa-Screen_Shot_2020-03-09_at_4.13.20_PM.png" title="Navigate to the 'SSH public keys' settings page" />

Next, click the "+ New Key" button to create a new SSH key for the repository.

<Lightbox src="/img/docs/dbt-cloud/cloud-configuring-dbt-cloud/6d8e980-Screen_Shot_2020-03-09_at_4.13.27_PM.png" title="Click the '+ New Key' button to create a new SSH key for the repository." />

Pick a descriptive name for the key and then paste in the deploy key generated by dbt Cloud for your repository. After saving this SSH key, dbt Cloud will be able to read and write files in your Azure DevOps repository.

<Lightbox src="/img/docs/dbt-cloud/cloud-configuring-dbt-cloud/d19f199-Screen_Shot_2020-03-09_at_4.13.50_PM.png" title="Enter and save the public key generated for your repository by dbt Cloud" />

### Other git providers

Don't see your git provider here? Please contact support - we're happy to help you set up dbt Cloud with any supported git provider.

## Limited integration
Some features of dbt Cloud require a tight integration with your git host, e.g. updating Github pull requests with dbt Cloud run statuses. Importing your project by a URL prevents you from using these features.

Once you give dbt Cloud access to your repository, you can continue to set up your project by adding a connection and creating and running your first dbt Cloud job.