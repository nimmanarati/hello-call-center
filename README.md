# hello-call-center
POC implementation to call center, robocall and junk SMS issue that is happening in Thailand

There could be many implementation to assume since this is not existed. 
1. run via Telco api webhook
2. run on mobile device


Feel free to add your own.

## Single Function Approach
I would like to start with the simplest version with a single function that take in `metadata`, `sms_content`/`call_content` and return `True` or `False` where `True` means the call/sms will forword to the phone and `False` means the call will log and sent to quarantine for user to inspect themself.  

e.g. function would structure like this
```python
def handle_sms(metadata, sms_content):
    flag = True
    flag |= check_if_from(metadata, "COMFORTCASH")
    
    flag |= check_if_contain(sms_content, "SEXY บาคาร่า")
    flag |= check_if_contain(sms_content, "EM199.com")
    
    return flag
    
def handle_call(metadata, call_content):
    flag = True
    flag |= check_if_in_blocklist(metadata)
    
    # filter 'คุณมีพัศดุติดที่ศุลกากกร กด 9 เพื่อติดต่อเจ้าหน้าที่'
    audio_hash = hash_audio(call_content)
    flag |= check_hash(audio_hash)
    
    return flag
  
```
