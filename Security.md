

### ROUTERs & SWITCHs
```
ENA
CONFI TE
ENABLE PASSWORD redes2
LINE VTY 0 7 
LOGIN
PASSWORD redes2
EXIT
```

```
LINE CONSOLE 0 
PASSWORD redes2
LOGIN
EXIT
```

```
SERVICE PASSWORD-ENCRYPTION
```

```
BANNER MOTD `#accesso_restringido#`
EXIT
EXIT
```

### SSH