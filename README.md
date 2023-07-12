---
jupyter:
  kernelspec:
    display_name: Python 3 (ipykernel)
    language: python
    name: python3
  language_info:
    codemirror_mode:
      name: ipython
      version: 3
    file_extension: .py
    mimetype: text/x-python
    name: python
    nbconvert_exporter: python
    pygments_lexer: ipython3
    version: 3.11.1
  nbformat: 4
  nbformat_minor: 5
---

::: {#e407a8e8 .cell .code execution_count="3"}
``` python
from symbolsearch import SearchScrip
import logging
```
:::

::: {#26c9776c .cell .code execution_count="5"}
``` python
logging.basicConfig(level=logging.DEBUG)
```
:::

::: {#acedb18b .cell .code execution_count="6"}
``` python
sc = SearchScrip()
```
:::

::: {#3596c760 .cell .markdown}
    Now its needed to initialize symbols of the required exchanges. 

    It will not not download the symbolmaster for a exchange within the same day unless

    it is specified by using hard_refresh=True
:::

::: {#bffb2ceb .cell .code execution_count="8"}
``` python
exch_list = ['NSE', 'NFO']
sc.initialize_symbols(exch_list=exch_list)
```
:::

::: {#be69b37a .cell .markdown}
get_expiry(exch, instrument, symbol, expiry) By default, it returns
current expiry of banknifty options
:::

::: {#591a028e .cell .code execution_count="9"}
``` python
sc.get_expiry()
```

::: {.output .execute_result execution_count="9"}
    datetime.date(2023, 7, 13)
:::
:::

::: {#b6c62352 .cell .code execution_count="10"}
``` python
sc.get_expiry(exch='NFO', instrument='FUTIDX', symbol='FINNIFTY',expiry='current')
```

::: {.output .execute_result execution_count="10"}
    datetime.date(2023, 7, 25)
:::
:::

::: {#65414df4 .cell .markdown}
search_scrip(exch, \*\*kwargs)

    The function will return in 3 different ways depending on the inputs

    1. if **kwargs params are symbol, instrument, optiontype, expiry, strikeprice then it 
    will return corresponding tradingsymbol and token

    2. if **kwargs params are same as point 1 but lacks any of the input then it will 
    return a dict of  tradingsymbols and tokens

    3. if **kwargs input is tradingsymbol then it will return the corresponding token
:::

::: {#06e0dd90 .cell .code execution_count="11"}
``` python
sc.search_scrip(exch='NFO', symbol='BANKNIFTY', instrument='OPTIDX', 
                optiontype='CE', expiry="13-7-2023", strikeprice=44000)
```

::: {.output .execute_result execution_count="11"}
    array(['BANKNIFTY13JUL23C44000', 41702], dtype=object)
:::
:::

::: {#d6fe86da .cell .code execution_count="12"}
``` python
sc.search_scrip(exch='NFO', symbol='BANKNIFTY', instrument='OPTIDX', 
                expiry="13-7-2023", strikeprice=44000)
```

::: {.output .execute_result execution_count="12"}
    {'BANKNIFTY13JUL23P44000': 41703, 'BANKNIFTY13JUL23C44000': 41702}
:::
:::

::: {#d4ab4cc4 .cell .code execution_count="13"}
``` python
sc.search_scrip(exch='NFO', tradingsymbol='BANKNIFTY13JUL23C44000')
```

::: {.output .execute_result execution_count="13"}
    41702
:::
:::

::: {#a8596802 .cell .markdown}
get_tradingsymbol(exch, \*\*kwargs)

    It will return tradingsymbol

    **kwargs params are symbol, instrument, optiontype, strikeprice, expiry for 'NFO', 
    'MCX' & 'CDS'

    **kwargs params are symbol, instrument for 'NSE'
:::

::: {#903d2247 .cell .code execution_count="14"}
``` python
sc.get_tradingsymbol(exch='NFO', symbol='BANKNIFTY', instrument='OPTIDX', 
                optiontype='CE', expiry="13-7-2023", strikeprice=44000)
```

::: {.output .execute_result execution_count="14"}
    'BANKNIFTY13JUL23C44000'
:::
:::

::: {#b54f25ba .cell .code execution_count="15"}
``` python
sc.get_tradingsymbol(exch='NSE', symbol='HDFC', instrument='EQ')
```

::: {.output .execute_result execution_count="15"}
    'HDFC-EQ'
:::
:::

::: {#45ca5390 .cell .markdown}
get_lotsize(exch, \*\*kwargs)

    Returns lotsize of the given symbols depending upon the inputs

    1. **kwargs -> tradingsymbol

    2. **kwargs -> symbol, expiry

    3. **kwargs -> symbol (lacks accuracy as it will return the lotsize 
            regardless of expiry.)
:::

::: {#9aa566cf .cell .code execution_count="16"}
``` python
sc.get_lotsize(exch='NFO', symbol='BANKNIFTY')
```

::: {.output .execute_result execution_count="16"}
    25
:::
:::

::: {#892b7f77 .cell .code execution_count="17"}
``` python
sc.get_lotsize(exch='NFO', symbol='BANKNIFTY', expiry='27-7-2023')
```

::: {.output .execute_result execution_count="17"}
    15
:::
:::
