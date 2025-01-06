Obsidian for private (remote) use
=================================

Private Obsidian rdesktop environment using [Tailscale](https://tailscale.com). 
This is imported from `gbraad-apps/personal-obsidian` but provides a more generic image.


## Usage instructions

```shell
$ podman run -d --name obsidian \
   --hostname ${HOSTNAME}-obsidian -p 8444:8444 \
   -v ~/Documents:/home/obsidian/Documents \
   ghcr.io/spotsnel-apps/obsidian:latest
```

This allows you to open the remote session from your IP, like
`https://[remote_ip]:8444`. 

> [!NOTE]
> Username: `obsidian`  
> Password: `password`

Otherwise, you can use tailscale to allow remote use:

```shell
$ podman exec obsidian tailscale up
$ tailscale ip
```

... and then open `https://[tailscale_ip]:8444`

### Devcontainer

A devcontainer is available for testing purposes. While it starts, the kasmvnc server
can not be used on localhost. Preferably the following can be done

As `root`
```
$ tmux new-session -s tailscaled -d
$ tmux send -t tailscaled "tailscaled" ENTER
$ tailscale up
```

and then use another user:
```
$ su - forge
$ kasmvncserver
$ tailscale ip
```

... and then open `https://[tailscale_ip]:8444`


### Actions

It is also possible to run a remote instance on Actions, by adding a Tailscale authentication key in the repository secrets named `TAILSCALE_AUTHKEY` and start the `tailscale-rdesktop` workflow.

```
$ gh workflow run tailscale-rdesktop.yml
```

## Author

| [!["Gerard Braad"](http://gravatar.com/avatar/e466994eea3c2a1672564e45aca844d0.png?s=60)](http://gbraad.nl "Gerard Braad <me@gbraad.nl>") |
|---|
| [@gbraad](https://gbraad.nl/social)  |


### Sponsor
Become a patron or sponsor, by simply clicking one of these buttons

[![](https://c5.patreon.com/external/logo/become_a_patron_button.png)](https://www.patreon.com/gbraad)

[![Github Sponsorship](.github/github_sponsor_btn.svg)](https://github.com/sponsors/gbraad)

... or consider a small one-time donation to show appreciation

[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/gbraad)

[![PayPal Donate](https://www.paypalobjects.com/en_US/i/btn/btn_donate_SM.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=me%40gbraad%2enl&lc=US&item_name=gbraad&currency_code=USD&bn=PP%2dDonationsBF%3abtn_donate_SM%2egif%3aNonHosted)
