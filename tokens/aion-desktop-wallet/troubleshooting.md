---
title: "Troubleshooting"
excerpt: "If you run into problems with your Aion Wallet, we're here to help!"
---
## I've Forgotten My Password

If you forget the password to your Aion wallet, follow these steps to attempt to recover your wallet. You need to have your `mnemonic` / `seed phrase` ready. If you do not have access to your `mnemonic` / `seed phrase`, or can't remember it, then unfortunately you cannot recover you wallet.

These instructions differ slightly between [Mac/Linux](#section-linux-and-mac) and [Windows](#section-windows).

### Linux and Mac

1. Open a terminal window.
2. Run `mv ~/.aion ~/.aion-old`.
3. Open the Aion wallet application.
4. Click **Add account**.
5. Under **Recover from seed**, enter your **Mnemonic**.
6. Enter a new **Password**.
7. Click **Recover**.
8. If your account is now listed on the **Accounts** page, run the following command to delete your old wallet information: `rm ~/.aion-old`.

### Windows

1. Go to your **Documents** folder.
2. Turn on **Show hidden files and folders**.
3. Rename `.aion` to `.aion-old`.
4. Open the Aion wallet application.
5. Click **Add account**.
6. Under **Recover from seed**, enter your **Mnemonic**.
7. Enter a new **Password**.
8. Click **Recover**.
9. If your account is now listed on the **Accounts** page, go back to your **Documents** folder and delete the `.aion-old` folder.

## Obtaining Logs

If our support team have requested logs off you, follow the process for the operating system to retrieve them.

### Linux / macOS

The `log` file is stored at `~/.aion/logs`. You can copy the contents of the folder to your Desktop by running `cp -r ~/.aion/logs ~/Desktop`. You may need to run this command as `sudo`. The `log` file is now on your Desktop.

You can now email this file to [support@aion.network](mailto:support@aion.network) when requested.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0a6c5a3-mac-copy-logs.gif",
        "mac-copy-logs.gif",
        745,
        384,
        "#202020"
      ],
      "caption": "Running the copy command and then viewing the contents of a file in a terminal."
    }
  ]
}
[/block]

### Windows

To view the Aion Desktop Wallet logs in Windows, navigate to `c:\Users\YOUR_USERNAME\.aion\log` replacing `YOUR_USERNAME` with your Windows username. In this example, my username is `John` so the address to my logs is `C:\Users\John\.aion\log`.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e6d03b3-windows-go-to-logs.gif",
        "windows-go-to-logs.gif",
        860,
        520,
        "#ebf0f3"
      ],
      "caption": "Finding the Aion Desktop Wallet logs in Windows 10."
    }
  ]
}
[/block]
You may need to [enable viewing of hidden files and folders](//support.microsoft.com/en-ca/help/4028316/windows-view-hidden-files-and-folders-in-windows-10).
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a404006-hidden_files_and_folders.gif",
        "hidden_files_and_folders.gif",
        520,
        293,
        "#032345"
      ],
      "caption": "Viewing hidden files and folders in Windows 10. Copyright [Microsoft](https://support.microsoft.com/en-ca/help/4028316/windows-view-hidden-files-and-folders-in-windows-10)"
    }
  ]
}
[/block]
You can now email this file to [support@aion.network](mailto:support@aion.network) when requested.

## Problems with Ledger

If you're having problems connecting your Ledger wallet to your Aion wallet, take a look at the troubleshooting steps below.

1. Make sure that the Aion app is installed on your Ledger wallet. Ledger have posted a guide on [how to install the Aion app](https://support.ledgerwallet.com/hc/en-us/articles/360008599834-Aion-AION-).
2. You need to have the Aion app **open** on your Ledger wallet when you connect. Open the Aion app on the Ledger and _then_ try to connect.
3. Make sure that the **contract data** is set to **on** within the Aion app on your Ledger.

If you're still having issues after following these steps, please reach out to us at [support@aion.network](mailto:support@aion.network) or through any of [our community groups](http://aion.network/community/). We have encountered a decent amount of issues with Ledger in the latest Aion Desktop Wallet build, are we're currently trying to find a solution.

## Windows and Antivirus Software

Due to the nature and fast release of the Aion Desktop Wallet, the `.exe` is not signed. This can cause certain installations of Windows and / or antivirus software such as McAfee and AVG to flag the wallet as malicious.

You may also encounter the following error: `CreateProcess failed code: 1450 insufficient system resources exist to complete the requested service.`

We recommend validating your download, and then adding exception in your antivirus software for the Aion Desktop Wallet. The exception can be made temporarily until you have completed the swap process.