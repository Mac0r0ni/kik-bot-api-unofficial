# Kik Bot API #
This fork just adds in the [Kik-API-Modifications, Made by vilq](https://github.com/VyIq/Kik-API-Modifications), and maybe some other few things from time to time.
Stored here for ease of use.

Use this library to develop bots for [Kik Messenger](https://www.kik.com) that are essentially automated humans.

It basically lets you do the same things as the offical Kik app by pretending to be a real smartphone client; It communicates with Kik's servers at `talk1110an.kik.com:5223` over a modified version of the [XMPP](https://xmpp.org/about/technology-overview.html) protocol.

This is the new branch of this project and is recommended.
## Installation and dependencies ##
First, make sure you are using **Python 3.6+**, not python 2.7. Second, just install it directly from GitHub:
```
git clone -b new https://github.com/Mac0r0ni/kik-bot-api-unofficial
pip3 install ./kik-bot-api-unofficial
```
## Usage ##
Examples are a great way to understand things. A good place to start is the `examples/` directory. 

It is as simple as:
```python
from kik_unofficial.client import KikClient
from kik_unofficial.callbacks import KikClientCallback
import kik_unofficial.datatypes.xmpp.chatting as chatting

class EchoBot(KikClientCallback):
    def __init__(self):
        self.client = KikClient(self, "your_kik_username", "your_kik_password")

    def on_authenticated(self):
        self.client.request_roster() # request list of chat partners

    def on_chat_message_received(self, chat_message: chatting.IncomingChatMessage):
        self.client.send_chat_message(chat_message.from_jid, 'You said "{}"!'.format(chat_message.body))
```
Currently Supported Operations:
- Log in with kik username and password, retrieve user information (such as email, name, etc).
- Fetch chat partners information
- Send text messages to users/groups and listen for incoming messages
- Send and receive 'is-typing' status
- Send and receive read receipts
- Fetch group information (name, participants, etc.)
- Fetch past message history
- Admin groups (add, remove or ban members, etc)
- Search for groups and join them [Experimental]
- Receive media content: camera, gallery, stickers
- Add a kik user as a friend
- Send images (including GIFs, using a tendor.com API key)

Sending videos or recordings is not supported yet.

## More functionality
Before investigating the format of certain requests/responses, it's worth checking if they are already documented in the [Message Formats](https://github.com/tomer8007/kik-bot-api-unofficial/wiki/Message-Formats) wiki page.

## Added


chatting.py Modifications
Added OutgoingSticker class
Added OutgoingSponsoredGIFMessage class
Added OutgoingFakeSystemMessage class
Added OutgoingFakeStatusMessage class
Added Tenor dev API key
Added OutgoingChatIPLogger class
Added OutgoingGroupIPLogger class
parsing_utilities.py Modifications
Added parse_sticker method - Thanks to Kief for insights into parsing <3
client.py Modifications
Added send_sponsored_gif_image method
Added send_sticker method
Added send_fake_system_message method
Added send_fake_status_message method
Added send_ip_logger method
Added join_group_with_invite_link method
roster.py Modifications
Added JoinByInviteLinkRequest class
