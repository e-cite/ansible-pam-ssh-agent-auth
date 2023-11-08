# Ansible Rolle "PAM SSH AGENT AUTH"

Installiert die PAM-Funktionalität, sich mittels SSH-Agent zu authentifizieren.

Dadurch kann sudo mittels SSH-Agent und ohne Passwort verwendet werden.

- https://manpages.debian.org/bookworm/libpam-ssh-agent-auth/index.html
- https://packages.debian.org/de/stable/libpam-ssh-agent-auth

## Anforderungen

- Es muss dennoch ein Become-Passwort für Ansible gesetzt werden. Dies kann
  durch die explizite Definition eines Fake Become-Passworts in den Group-Vars
  umgangen werden.
  ~~~yaml
  # Beispiel:
  ansible_become_pass: "foo"  # Fake Become-Password trotz pam_ssh_agent_auth
  ~~~

## Variablen

- `pam_ssh_agent_auth__sudo_keys`: (*Erforderlich*)

  SSH Public-Keys, mit welchen sudo-Berechtigungen gewährt werden.
  ~~~yaml
  # Beispiel:
  pam_ssh_agent_auth__sudo_keys:
  - "ssh-ed25519 <Public-Key> <name@host>"
  ~~~

## Abhängigkeiten

Keine.

## Beispiel

    - hosts: servers
      roles:
        - pam-ssh-agent-auth

## Lizenz

MIT
