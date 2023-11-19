
# Host Environment Construction Guide

* Install build tools

```bash
sudo pacman -S archiso
```

* Modify the configuration file

  * If you plan to use the KVM virtual machine as the host, no modification is required.
  * If you plan to use a virtual machine such as VirtualBox as a host, modify the value of the "harddrives" key in user_configureation.json to /dev/sda, /dev/sdb, or /dev/sdc.

* Create a configuration file directory for the build process

```bash
mkdir -p ./archiso
cd ./archiso
cp -r /usr/share/archiso/configs/releng/* ./
```

* Overwrite the configuration file in the configuration file directory.

```bash
cd ./archiso
cp -r path/to/rkos-build/airootfs ./
cp path/to/rkos-build/packages.x86_64 ./

```

* Build host image

```bash
cd ./archiso
mkarchiso -v -w work/ -o out/ ./
```

* Use kvm to run the built image to install the host system.

  * The configuration that needs to be confirmed is that three virtual disks must be configured. The first disk has a capacity of 20GB and is used for host system installation. The second disk is 30GB and is used as the target disk. The third disk is selected according to the actual situation. Block disk capacity plus memory capacity greater than 35GB
  * The installer will run automatically within about 5 minutes after the host image starts. After the installer starts, you need to manually select the install option, and you don’t need to set any options.
  * If it does not run automatically or runs incorrectly, execute the command manually: ```archinstall --config user_configuration.json --creds user_credentials.json --disk_layouts user_disk_layout.json```
  * After the installation is complete, you will be prompted whether to enter the chroot environment. Here,  you can choose no and then reboot.
  * After the host environment is installed, you need to manually mount the swap partition.
  * Host username root password root

* Automation script (Comming soon)

## References

[https://wiki.archlinux.org/title/archiso](https://wiki.archlinux.org/title/archiso)

[https://github.com/archlinux/archinstall](https://github.com/archlinux/archinstall)

[https://github.com/archlinux/archinstall/wiki/Building-and-Testing](https://github.com/archlinux/archinstall/wiki/Building-and-Testing)

# rkos

## Contribution

The `dagrs` project relies on community contributions and aims to simplify getting started. To develop `dagrs`, clone the repository, then install all dependencies, run the test suite and try it out locally. Pick an issue, make changes, and submit a pull request for community review.

### What's the contribution

Here are some guidelines for contributing to this project:

1. Report issues/bugs: If you find any issues or bugs in the project, please report them by creating an issue on the issue tracker. Describe the issue in detail and also mention the steps to reproduce it. The more details you provide, the easier it will be for me to investigate and fix the issue.
2. Suggest enhancements: If you have an idea to enhance or improve this project, you can suggest it by creating an issue on the issue tracker. Explain your enhancement in detail along with its use cases and benefits. I appreciate well-thought-out enhancement suggestions.
3. Contribute code: If you want to develop and contribute code, follow these steps:
   - Choose an issue to work on. Issues labeled `good first issue` are suitable for newcomers. You can also look for issues marked `help wanted`.
   - Fork the `dagrs` repository and create a branch for your changes.
   - Make your changes and commit them with a clear commit message. Sign the [Developer Certificate of Origin](https://developercertificate.org/) (DCO) by adding a `Signed-off-by` line to your commit messages. This certifies that you wrote or have the right to submit the code you are contributing to the project.
   - Push your changes to GitHub and open a pull request.
   - Respond to any feedback on your pull request. The `dagrs` maintainers will review your changes and may request modifications before merging. Please ensure your code is properly formatted and follows the same style as the existing codebase.
   - Once your pull request is merged, you will be listed as a contributor in the project repository and documentation.
4. Write tutorials/blog posts: You can contribute by writing tutorials or blog posts to help users get started with this project. Submit your posts on the issue tracker for review and inclusion. High quality posts that provide value to users are highly appreciated.
5. Improve documentation: If you find any gaps in the documentation or think any part can be improved, you can make changes to files in the documentation folder and submit a PR. Ensure the documentation is up-to-date with the latest changes.

Your contributions are highly appreciated. Feel free to ask any questions if you have any doubts or facing issues while contributing. The more you contribute, the more you will learn and improve your skills.

### DCO & PGP

To comply with the requirements, contributors must include both a `Signed-off-by` line and a PGP signature in their commit messages. You can find more information about how to generate a PGP key [here](https://docs.github.com/en/github/authenticating-to-github/managing-commit-signature-verification/generating-a-new-gpg-key).

Git even has a `-s` command line option to append this automatically to your commit message, and `-S` to sign your commit with your PGP key. For example:

```bash
$ git commit -S -s -m 'This is my commit message'
```

### Rebase the branch

If you have a local git environment and meet the criteria below, one option is to rebase the branch and add your Signed-off-by lines in the new commits. Please note that if others have already begun work based upon the commits in this branch, this solution will rewrite history and may cause serious issues for collaborators (described in the git documentation under “The Perils of Rebasing”).

You should only do this if:

- You are the only author of the commits in this branch
- You are absolutely certain nobody else is doing any work based upon this branch
- There are no empty commits in the branch (for example, a DCO Remediation Commit which was added using `-allow-empty`)

To add your Signed-off-by line to every commit in this branch:

- Ensure you have a local copy of your branch by checking out the pull request locally via command line.
- In your local branch, run: `git rebase HEAD~1 --signoff`
- Force push your changes to overwrite the branch: `git push --force-with-lease origin main`

## License

Freighter is licensed under this Licensed:

* MIT LICENSE ([LICENSE-MIT](LICENSE-MIT) or https://opensource.org/licenses/MIT)
* Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE) or https://www.apache.org/licenses/LICENSE-2.0)

## Contact us

Quanyi Ma <genedna@gmail.com>, Xiaoyu Jia <xyyy1420@gmail.com>