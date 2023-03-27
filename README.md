# GOV.UK EKS helpers

Shell scripts to help with doing things in GOV.UK's EKS infrastructure.

- [Installation](#installation)
- [Usage](#usage)
- [Recognised environments](#recognised-environments)

## Installation

1. If you haven't connected to EKS before, [set up the tools required to use the GOV.UK Kubernetes platform](https://govuk-k8s-user-docs.publishing.service.gov.uk/get-started/set-up-tools/).

2. Clone this repo locally.

    ```
    $ cd ~/govuk
    $ git clone git@github.com:ollietreend/govuk-eks-helpers.git
    ```

3. (optional) Add `~/govuk/govuk-eks-helpers/bin` to your `PATH`, so you can call the scripts from anywhere.

    Assuming you use ZSH:

    ```
    $ echo "export PATH=\$PATH:\$HOME/govuk/govuk-eks-helpers/bin" >> ~/.zshrc
    ```

    For this change to take effect, you'll need to open a new Terminal tab, or run:

    ```
    $ source ~/.zshrc
    ```

## Usage

### Open a Rails console

```
$ eks-console {environment} {app-name}
```

<details>
<summary><strong>Example</strong></summary>
<blockquote>

Open a Rails consosle on Whitehall in integration:

```
$ eks-console integration whitehall-admin
```

</blockquote>
</details>

### Run a Rake task

```
$ eks-rake {environment} {app-name} {rake-task}
```

<details>
<summary><strong>Example</strong></summary>
<blockquote>

Run a reslugging Rake task on Whitehall in integration:

```
$ eks-rake integration whitehall-admin reslug:person[old-slug,new-slug]
```

Get a list of available Rake tasks:

```
$ eks-rake integration whitehall-admin -T
```

</blockquote>
</details>

### Connect to a running container

```
$ eks-connect {environment} {app-name} {command}
```

Use this command if you want to open a `bash` shell to the container (effectively recreating an SSH experience), or run any other command on the container.

<details>
<summary><strong>Example</strong></summary>
<blockquote>

Open a `bash` shell on Whitehall in integration:

```
$ eks-connect integration whitehall-admin bash
```

Commands that contain spaces need to be wrapped in quote marks. For example:

```
$ eks-connect integration whitehall-admin "ls -lh"
```

</blockquote>
</details>

## Recognised environments

There are three GOV.UK EKS environments: `integration`, `staging` and `production`.

These scripts also recognise 'short hand' versions of the environments – where they'll match, so long as it partially matches the beginning of a valid environment.

For example, you can connect to integration by simply using the letter `i`:

```
$ eks-console i whitehall-admin
```

Which is functionally the same as:

```
$ eks-console integration whitehall-admin
```
