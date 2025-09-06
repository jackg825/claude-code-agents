# Claude Code Hooks Examples

This document provides examples for setting up notification hooks in Claude Code to get alerts when Claude needs your input or completes tasks.

## Overview

Claude Code hooks allow you to run custom commands in response to specific events. Notification hooks are particularly useful for:
- Getting alerts when Claude finishes a task and needs input
- Being notified when Claude stops working and is ready for new instructions
- Staying informed about long-running operations

## Hook Event Types

- **`Notification`**: Triggered when Claude needs your input or attention
- **`Stop`**: Triggered when Claude completes a task and is ready for new input

## macOS Examples

### Basic macOS Notifications (terminal-notifier)

First install terminal-notifier if you haven't already:
```bash
brew install terminal-notifier
```

Basic configuration for macOS with Warp terminal:

```json
{
  "hooks": {
    "Notification": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "terminal-notifier -title Claude -message 'Needs your input' -sound Glass -activate dev.warp.Warp-Stable -ignoreDnD"
          }
        ]
      }
    ],
    "Stop": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "terminal-notifier -title Claude -message 'Ready for input' -sound Pop -activate dev.warp.Warp-Stable"
          }
        ]
      }
    ]
  }
}
```

### Advanced macOS Notifications

More detailed notifications with custom sounds and actions:

```json
{
  "hooks": {
    "Notification": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "terminal-notifier -title '🤖 Claude Code' -subtitle 'Waiting for Input' -message 'Claude has paused and needs your response' -sound Glass -activate dev.warp.Warp-Stable -ignoreDnD -timeout 10"
          }
        ]
      }
    ],
    "Stop": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "terminal-notifier -title '✅ Claude Code' -subtitle 'Task Complete' -message 'Ready for your next instruction' -sound Pop -activate dev.warp.Warp-Stable -timeout 5"
          }
        ]
      }
    ]
  }
}
```

### macOS with Different Terminal Apps

#### iTerm2
```json
{
  "hooks": {
    "Notification": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command", 
            "command": "terminal-notifier -title Claude -message 'Needs your input' -sound Glass -activate com.googlecode.iterm2"
          }
        ]
      }
    ]
  }
}
```

#### Terminal.app
```json
{
  "hooks": {
    "Notification": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "terminal-notifier -title Claude -message 'Needs your input' -sound Glass -activate com.apple.Terminal"
          }
        ]
      }
    ]
  }
}
```

## Windows Examples

### Windows Toast Notifications (PowerShell)

```json
{
  "hooks": {
    "Notification": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "powershell -Command \"[Windows.UI.Notifications.ToastNotificationManager, Windows.UI.Notifications, ContentType = WindowsRuntime] > $null; $template = [Windows.UI.Notifications.ToastNotificationManager]::GetTemplateContent([Windows.UI.Notifications.ToastTemplateType]::ToastText02); $template.SelectSingleNode('//text[@id=\\\"1\\\"]').AppendChild($template.CreateTextNode('Claude Code')); $template.SelectSingleNode('//text[@id=\\\"2\\\"]').AppendChild($template.CreateTextNode('Needs your input')); $toast = [Windows.UI.Notifications.ToastNotification]::new($template); [Windows.UI.Notifications.ToastNotificationManager]::CreateToastNotifier('Claude Code').Show($toast)\""
          }
        ]
      }
    ],
    "Stop": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "powershell -Command \"[Windows.UI.Notifications.ToastNotificationManager, Windows.UI.Notifications, ContentType = WindowsRuntime] > $null; $template = [Windows.UI.Notifications.ToastNotificationManager]::GetTemplateContent([Windows.UI.Notifications.ToastTemplateType]::ToastText02); $template.SelectSingleNode('//text[@id=\\\"1\\\"]').AppendChild($template.CreateTextNode('Claude Code')); $template.SelectSingleNode('//text[@id=\\\"2\\\"]').AppendChild($template.CreateTextNode('Ready for input')); $toast = [Windows.UI.Notifications.ToastNotification]::new($template); [Windows.UI.Notifications.ToastNotificationManager]::CreateToastNotifier('Claude Code').Show($toast)\""
          }
        ]
      }
    ]
  }
}
```

### Windows with WSL notify-send

If using WSL with a notification daemon:

```json
{
  "hooks": {
    "Notification": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "wsl notify-send 'Claude Code' 'Needs your input' -u normal -t 5000"
          }
        ]
      }
    ],
    "Stop": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command", 
            "command": "wsl notify-send 'Claude Code' 'Ready for input' -u normal -t 3000"
          }
        ]
      }
    ]
  }
}
```

## Linux Examples

### Linux Desktop Notifications (notify-send)

```json
{
  "hooks": {
    "Notification": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "notify-send 'Claude Code' 'Needs your input' -u normal -t 5000 -i dialog-information"
          }
        ]
      }
    ],
    "Stop": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "notify-send 'Claude Code' 'Ready for input' -u normal -t 3000 -i dialog-information"
          }
        ]
      }
    ]
  }
}
```

### Linux with Sound

```json
{
  "hooks": {
    "Notification": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "notify-send 'Claude Code' 'Needs your input' -u normal -t 5000 && paplay /usr/share/sounds/alsa/Front_Left.wav"
          }
        ]
      }
    ],
    "Stop": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "notify-send 'Claude Code' 'Ready for input' -u normal -t 3000 && paplay /usr/share/sounds/alsa/Front_Right.wav"
          }
        ]
      }
    ]
  }
}
```

## Advanced Hook Configurations

### Conditional Notifications with Matchers

You can use matchers to create different notifications for different scenarios:

```json
{
  "hooks": {
    "Notification": [
      {
        "matcher": "error",
        "hooks": [
          {
            "type": "command",
            "command": "terminal-notifier -title '⚠️ Claude Code Error' -message 'An error occurred - check console' -sound Basso -activate dev.warp.Warp-Stable"
          }
        ]
      },
      {
        "matcher": "test",
        "hooks": [
          {
            "type": "command",
            "command": "terminal-notifier -title '🧪 Claude Code Tests' -message 'Test results ready for review' -sound Ping -activate dev.warp.Warp-Stable"
          }
        ]
      },
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "terminal-notifier -title 'Claude Code' -message 'Needs your input' -sound Glass -activate dev.warp.Warp-Stable"
          }
        ]
      }
    ]
  }
}
```

### Multiple Commands per Hook

Run multiple commands for a single hook event:

```json
{
  "hooks": {
    "Notification": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "terminal-notifier -title Claude -message 'Needs input' -sound Glass"
          },
          {
            "type": "command", 
            "command": "osascript -e 'display notification \"Claude is waiting for input\" with title \"Claude Code\"'"
          },
          {
            "type": "command",
            "command": "echo 'Claude needs input' >> ~/claude-notifications.log"
          }
        ]
      }
    ]
  }
}
```

### Time-based Notifications

Different notifications for different times of day:

```json
{
  "hooks": {
    "Notification": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "if [ $(date +%H) -ge 22 ] || [ $(date +%H) -le 7 ]; then terminal-notifier -title Claude -message 'Needs input (quiet mode)' -sound --silent -activate dev.warp.Warp-Stable; else terminal-notifier -title Claude -message 'Needs input' -sound Glass -activate dev.warp.Warp-Stable; fi"
          }
        ]
      }
    ]
  }
}
```

## Custom Sound Files

### macOS Custom Sounds

Place custom sound files in `~/Library/Sounds/` and reference them:

```json
{
  "hooks": {
    "Notification": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "terminal-notifier -title Claude -message 'Needs input' -sound 'Custom Sound Name' -activate dev.warp.Warp-Stable"
          }
        ]
      }
    ]
  }
}
```

### Available macOS System Sounds

Common system sounds you can use:
- `Basso` - Error/warning sound
- `Blow` - Gentle notification
- `Bottle` - Pop sound
- `Frog` - Unique notification
- `Funk` - Modern notification
- `Glass` - Clean notification (recommended)
- `Hero` - Achievement sound
- `Morse` - Attention-getting
- `Ping` - Light notification
- `Pop` - Quick notification
- `Purr` - Subtle notification
- `Sosumi` - Classic Mac sound
- `Submarine` - Deep notification
- `Tink` - Light metallic sound

## Troubleshooting

### Common Issues

1. **Terminal app not activating**: Check the exact bundle ID with:
   ```bash
   osascript -e 'id of app "Warp"'
   ```

2. **Notifications not showing**: Ensure notification permissions are enabled in System Preferences.

3. **Commands not found**: Verify the notification tool is installed:
   ```bash
   which terminal-notifier
   which notify-send
   ```

4. **Sounds not playing**: Check volume settings and sound file paths.

### Testing Your Configuration

Test your hooks manually:

```bash
# macOS
terminal-notifier -title "Test" -message "Hook test" -sound Glass

# Linux  
notify-send "Test" "Hook test"

# Windows
powershell -Command "Add-Type -AssemblyName System.Windows.Forms; [System.Windows.Forms.MessageBox]::Show('Hook test', 'Test')"
```

## Installation Instructions

### Adding Hooks to Claude Code

1. Open Claude Code settings/preferences
2. Navigate to the hooks configuration section
3. Paste your JSON configuration
4. Save and restart Claude Code if necessary

### Configuration File Location

Hooks are typically stored in your Claude Code configuration file. Check these locations:

- **macOS**: `~/Library/Application Support/Claude Code/config.json`
- **Windows**: `%APPDATA%/Claude Code/config.json`
- **Linux**: `~/.config/claude-code/config.json`

## Best Practices

1. **Use appropriate sound levels**: Consider using quieter sounds for frequent notifications
2. **Set timeouts**: Use `-timeout` (macOS) or `-t` (Linux) to auto-dismiss notifications
3. **Test thoroughly**: Verify hooks work before relying on them for important work
4. **Consider context**: Use matchers to provide relevant notifications for different situations
5. **Respect system settings**: Use `-ignoreDnD` thoughtfully to avoid interrupting Do Not Disturb mode

## Contributing

If you have additional notification hook examples for other platforms or tools, please contribute them to help the community!