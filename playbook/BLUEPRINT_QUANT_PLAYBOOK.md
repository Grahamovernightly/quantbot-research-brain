# See primary copy
The canonical playbook is maintained at:
/Users/g/Documents/EA L2 data/BLUEPRINT_QUANT_PLAYBOOK.md

Key excerpt — Three EA Families:

## Family A — STRUCTURAL_MEAN_REVERTERS
Symbols: AUDNZD, EURGBP, EURCHF, CADCHF, AUDCAD
Purpose: Always-on, funded accounts, consistent extraction
Params: PipStep 8-16, LotSizeExp 1.0-1.1, MaxOrders 10-15
Tag: funded_structural

## Family B — SESSION_HARVESTERS  
Symbols: EURJPY, GBPJPY, GBPCAD
Purpose: Challenge accounts, aggressive profit targeting
Params: PipStep 14-26, LotSizeExp 1.2-1.3, MaxOrders 15-22
Tag: challenge_session

## Family C — REGIME_OPPORTUNISTS
Symbols: EURUSD, GBPUSD, USDCAD, NZDUSD, USDJPY, USDCHF
Purpose: Activated when Hurst<0.48 AND ADX<22 confirmed
Params: Dynamic per regime classification
Tag: regime_opportunist
