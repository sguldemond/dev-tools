# Development tools
Collection of useful tools for development


## Git

### [pre-commit](https://pre-commit.com/)

My pre-commit configuration for a Python project:
```
repos:
- repo: https://github.com/pre-commit/pre-commit-hooks
  rev: v2.4.0
  hooks:
  -   id: trailing-whitespace
  -   id: end-of-file-fixer
  -   id: check-yaml
  -   id: check-added-large-files

- repo: https://github.com/psf/black
  rev: stable
  hooks:
    - id: black
      language_version: python3.8

- repo: https://github.com/pre-commit/mirrors-mypy
  rev: ''  # Use the sha / tag you want to point at
  hooks:
  -   id: mypy
```

Run pre-commit on a folder:
```
$ git ls-files -- project1 | xargs pre-commit run --files
```

## Python

### Keeping pip packages up-to-date
- [Stack overflow topic](https://stackoverflow.com/questions/2720014/how-to-upgrade-all-python-packages-with-pip)
- [pip-review](https://github.com/jgonggrijp/pip-review)
- [pipupgrade](https://github.com/achillesrasquinha/pipupgrade)

### Setting environment variables in virtual environment

Add custom env vars to activate script:
```
$ cat .env
export FOO=bar
$ cat .env >> venv/bin/activate
```

### VSCode settings

- [Black](https://github.com/psf/black) as formatting standard
- [Jedi](https://github.com/davidhalter/jedi) for better autocompletion then Pylance
```
$ cat .vscode/settings.json
{
    "python.formatting.provider": "black",
    "python.languageServer": "Jedi"
}
```

## Certbot

### Create certificates

```
$ certbot certonly --standalone -d foo.bar.com
```

### Auto renew certificates (still testing)

```
$ cat renew.sh
docker stop container-on-port-80-and-443
sudo certbot renew
docker start container-on-port-80-and-443

$ sudo crontab -e
0 0 */9 * * bash /dir/renew.sh > /dir/cron.log (check every 9 days for renewal)
```


