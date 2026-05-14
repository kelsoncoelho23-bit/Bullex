instrument{name="Kelson",
short_name="Kelson",
icon="", overlay=true}
-- Configuraes do usurio
input_group {"CORES", call_color = input{default = "#00ff00", type = input.color, title = "Cor CALL"}}
input_group {"CORES", put_color = input{default = "#ff0000", type = input.color, title = "Cor PUT"}}
-- Parmetros tcnicos
sma_period = input{default = 14, title = "Perodo SMA"}
bb_multiplier = input{default = 2.5, title = "Multiplicador BB"}
stdev_period = input{default = 20, title = "Perodo Desvio"}
-- Clculos tcnicos
smaa = sma(close, sma_period)
upper_band = smaa + (stdev(close, stdev_period) * bb_multiplier)
lower_band = smaa - (stdev(close, stdev_period) * bb_multiplier)
-- Padro: Reverso de Alta (CALL)
plot_shape(open[4] > close[4] and open[3] > close[3] and open[2] > close[2] and open[1] < close[1] and close[1] > lower_band[1],
    "Call_Rev_Alta",
    shape_style.arrowup,
    shape_size.large,
    call_color,
    shape_location.belowbar,
    -1,
    "Compra",
    "white"
)
-- Padro: Reverso de Baixa (PUT)
plot_shape(open[4] < close[4] and open[3] < close[3] and open[2] < close[2] and open[1] > close[1] and close[1] < upper_band[1],
    "Put_Rev_Baixa",
    shape_style.arrowdown,
    shape_size.large,
    put_color,
    shape_location.abovebar,
    -1,
    "Vender",
    "white"
)
