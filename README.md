Input

PeriodoStop(3);
ExecutarAoLigar(true);
GridDinamico(true);
Contratos(1);
Compra(true);
Venda(true);
DistanciaEntreNiveis(10);
stop (5000);


Var

Atr1, Atr2, Atr3 : Float;
SinalC, SinalV : Boolean;
n1, n2, n3, n4, n5,n6,n7,n8,n9,n10,n11,n12,n13,n14,n15,n16,n17,n18,n19,n20,n21,n22,n23,n24,n25,n26,n27,n28,n29,n30,hilox,agr,atr,v1,v2 : float;
nGrid, vMedia : float;
i,data_de_compra,data_de_expiração  : integer;


begin
   
begin
  hilox := hiloActivator(29);
 agr := AccAgressSaldo(0);
 atr := StopATR(20.00,250,0);
 v1 :=  AgressionVolBuy ;
  v2 :=  AgressionVolSell;
  Atr1 := StopAtr(1, 20, 0)|0|;
  Atr2 := StopAtr(2, 20, 0)|0|;
  Atr3 := StopAtr(3, 20, 0)|0|;
  SinalC:= ((Atr1 > Atr2) e (Atr2 > Atr3)) e ((Close > Atr1) e (Close > Atr2) e (Close > Atr3));
  SinalV:= ((Atr1 < Atr2) e (Atr2 < Atr3)) e ((Close < Atr1) e (Close < Atr2) e (Close < Atr3));

  Se SinalC entao PaintBar(ClLime);
  Se SinalV entao PaintBar(255);
  Plot(Atr1);
  Plot2(Atr2);
  Plot3(Atr3);

  //sistema de controle
  

begin

If Time >= 1700 then closePosition;

//----------------------------------------------------------------------------------//
// Faz com que o robô abra a ordem assim que for executado no módulo de automação
//----------------------------------------------------------------------------------// 
If ExecutarAoLigar then
  Begin
    If (not IsBought) e (not IsSold) then
      Begin
        If Compra then se (close>open) e  ((Atr1 > Atr2) e (Atr2 > Atr3)) e ((Close > Atr1) e (Close > Atr2) e (Close > Atr3))  entao BuyLimit (high[0] - 25,Contratos)
        Else If Venda then se (close<open) e ((Atr1 < Atr2) e (Atr2 < Atr3)) e ((Close < Atr1) e (Close < Atr2) e (Close < Atr3)) entao SellShortLimit(low[0] + 25,Contratos);
      End;
  End;

//----------------------------------------------------------------------------------//
// Captura o preço de abertura da Posição atual para montagem do Gradiente Linear   // 
//----------------------------------------------------------------------------------//
  If (not IsSold[1]) e IsSold then
    Begin
      n1 := SellPrice;
      n2 := n1 + (DistanciaEntreNiveis * MinPriceIncrement);
      n3 := n1 + ((2 * DistanciaEntreNiveis) * MinPriceIncrement);
      n4 := n1 + ((3 * DistanciaEntreNiveis) * MinPriceIncrement);
      n5 := n1 + ((4 * DistanciaEntreNiveis) * MinPriceIncrement);
      n6 := n1 + ((5 * DistanciaEntreNiveis) * MinPriceIncrement);
      n7 := n1 + ((6 * DistanciaEntreNiveis) * MinPriceIncrement);
      n8 := n1 + ((7 * DistanciaEntreNiveis) * MinPriceIncrement);
      n9 := n1 + ((8 * DistanciaEntreNiveis) * MinPriceIncrement);
      n10 := n1 + ((9 * DistanciaEntreNiveis) * MinPriceIncrement);
      n11 := n1 + ((10 * DistanciaEntreNiveis) * MinPriceIncrement);
      n12 := n1 + ((11 * DistanciaEntreNiveis) * MinPriceIncrement);
      n13 := n1 + ((12 * DistanciaEntreNiveis) * MinPriceIncrement);
      n14 := n1 + ((13 * DistanciaEntreNiveis) * MinPriceIncrement);
      n15 := n1 + ((14 * DistanciaEntreNiveis) * MinPriceIncrement);
      n16 := n1 + ((15 * DistanciaEntreNiveis) * MinPriceIncrement);
      n17 := n1 + ((16 * DistanciaEntreNiveis) * MinPriceIncrement);
      n18 := n1 + ((17 * DistanciaEntreNiveis) * MinPriceIncrement);
      n19 := n1 + ((18 * DistanciaEntreNiveis) * MinPriceIncrement);
      n20 := n1 + ((19 * DistanciaEntreNiveis) * MinPriceIncrement);
      n21 := n1 + ((20 * DistanciaEntreNiveis) * MinPriceIncrement);
      n22 := n1 + ((21 * DistanciaEntreNiveis) * MinPriceIncrement);
      n23 := n1 + ((22 * DistanciaEntreNiveis) * MinPriceIncrement);
      n24 := n1 + ((23 * DistanciaEntreNiveis) * MinPriceIncrement);
      n25 := n1 + ((24 * DistanciaEntreNiveis) * MinPriceIncrement);
      n26 := n1 + ((25 * DistanciaEntreNiveis) * MinPriceIncrement);
      n27 := n1 + ((26 * DistanciaEntreNiveis) * MinPriceIncrement);
      n28 := n1 + ((27 * DistanciaEntreNiveis) * MinPriceIncrement);
      n29 := n1 + ((28 * DistanciaEntreNiveis) * MinPriceIncrement);
      n30 := n1 + ((29 * DistanciaEntreNiveis) * MinPriceIncrement);

    End
  else if (not IsBought[1]) e IsBought then
    Begin
      n1 := BuyPrice;
      n2 := n1 - (DistanciaEntreNiveis * MinPriceIncrement);
      n3 := n1 - ((2 * DistanciaEntreNiveis) * MinPriceIncrement);
      n4 := n1 - ((3 * DistanciaEntreNiveis) * MinPriceIncrement);
      n5 := n1 - ((4 * DistanciaEntreNiveis) * MinPriceIncrement);
      n6 := n1 - ((5 * DistanciaEntreNiveis) * MinPriceIncrement);
      n7 := n1 - ((6 * DistanciaEntreNiveis) * MinPriceIncrement);
      n8 := n1 - ((7 * DistanciaEntreNiveis) * MinPriceIncrement);
      n9 := n1 - ((8 * DistanciaEntreNiveis) * MinPriceIncrement);
      n10 := n1 - ((9 * DistanciaEntreNiveis) * MinPriceIncrement);
      n11 := n1 - ((10 * DistanciaEntreNiveis) * MinPriceIncrement);
      n12 := n1 - ((11 * DistanciaEntreNiveis) * MinPriceIncrement);
      n13 := n1 - ((12 * DistanciaEntreNiveis) * MinPriceIncrement);
      n14 := n1 - ((13 * DistanciaEntreNiveis) * MinPriceIncrement);
      n15 := n1 - ((14 * DistanciaEntreNiveis) * MinPriceIncrement);
      n16 := n1 - ((15 * DistanciaEntreNiveis) * MinPriceIncrement);
      n17 := n1 - ((16 * DistanciaEntreNiveis) * MinPriceIncrement);
      n18 := n1 - ((17 * DistanciaEntreNiveis) * MinPriceIncrement);
      n19 := n1 - ((18 * DistanciaEntreNiveis) * MinPriceIncrement);
      n20 := n1 - ((19 * DistanciaEntreNiveis) * MinPriceIncrement);
      n21 := n1 - ((20 * DistanciaEntreNiveis) * MinPriceIncrement);
      n22 := n1 - ((21 * DistanciaEntreNiveis) * MinPriceIncrement);
      n23 := n1 - ((22 * DistanciaEntreNiveis) * MinPriceIncrement);
      n24 := n1 - ((23 * DistanciaEntreNiveis) * MinPriceIncrement);
      n25 := n1 - ((24 * DistanciaEntreNiveis) * MinPriceIncrement);
      n26 := n1 - ((25 * DistanciaEntreNiveis) * MinPriceIncrement);
      n27 := n1 - ((26 * DistanciaEntreNiveis) * MinPriceIncrement);
      n28 := n1 - ((27 * DistanciaEntreNiveis) * MinPriceIncrement);
      n29 := n1 - ((28 * DistanciaEntreNiveis) * MinPriceIncrement);
      n30 := n1 - ((29 * DistanciaEntreNiveis) * MinPriceIncrement);

    End;

//----------------------------------------------------------------------------------//
// Faz a montagem do grid de forma dinâmica conforme o preço avança entre os níveis
//----------------------------------------------------------------------------------//
If GridDinamico then
  Begin
    If IsBought then  // Grid dinâmico quando está comprado
      Begin  
        If Position <= contratos then                                                
          if ((Close[1] <= n1) ou (Close[1] >= n1)) then BuyLimit(n2, Contratos);    
        If Position <= (contratos * 2) then
          if (Close <= n2) then BuyLimit(n3, Contratos);
        If Position <= (contratos * 3) then
          if (Close <= n3) then BuyLimit(n4, Contratos);
        If Position <= (contratos * 4) then
          if (Close <= n4) then BuyLimit(n5, Contratos);
          If Position <= (contratos * 5) then
          if (Close <= n5) then BuyLimit(n6, Contratos);
          If Position <= (contratos * 6) then
          if (Close <= n6) then BuyLimit(n7, Contratos);
          If Position <= (contratos *7) then
          if (Close <= n7) then BuyLimit(n8, Contratos);
          If Position <= (contratos * 8) then
          if (Close <= n8) then BuyLimit(n9, Contratos);
          If Position <= (contratos * 9) then
          if (Close <= n9) then BuyLimit(n10, Contratos);
          If Position <= (contratos * 10) then 
          if (Close <= n10) then BuyLimit(n11, Contratos);
          If Position <= (contratos * 11) then
          if (Close <= n11) then BuyLimit(n12, Contratos);
          If Position <= (contratos * 12) then
          if (Close <= n12) then BuyLimit(n13, Contratos);
          If Position <= (contratos * 13) then
          if (Close <= n13) then BuyLimit(n14, Contratos);
          If Position <= (contratos * 14) then
          if (Close <= n14) then BuyLimit(n15, Contratos);
          If Position <= (contratos * 15) then
          if (Close <= n15) then BuyLimit(n16, Contratos);
          If Position <= (contratos * 16) then
          if (Close <= n16) then BuyLimit(n17, Contratos);
          If Position <= (contratos * 17) then                  
          if (Close <= n17) then BuyLimit(n18, Contratos);
          If Position <= (contratos * 18) then
          if (Close <= n18) then BuyLimit(n19, Contratos);
          If Position <= (contratos * 19) then
          if (Close <= n19) then BuyLimit(n20, Contratos);
          If Position <= (contratos * 20) then
          if (Close <= n20) then BuyLimit(n21, Contratos);
          If Position <= (contratos * 21) then
          if (Close <= n21) then BuyLimit(n22, Contratos);
          If Position <= (contratos * 22) then
          if (Close <= n22) then BuyLimit(n23, Contratos);
          If Position <= (contratos * 23) then
          if (Close <= n23) then BuyLimit(n24, Contratos);
          If Position <= (contratos * 24) then
          if (Close <= n24) then BuyLimit(n25, Contratos);
          If Position <= (contratos * 25) then
          if (Close <= n25) then BuyLimit(n26, Contratos);
          If Position <= (contratos * 26) then
          if (Close <= n26) then BuyLimit(n27, Contratos);
          If Position <= (contratos * 27) then
          if (Close <= n27) then BuyLimit(n28, Contratos);
          If Position <= (contratos * 28) then
          if (Close <= n28) then BuyLimit(n29, Contratos);
          If Position <= (contratos * 29) then
          if (Close <= n29) then BuyLimit(n30, Contratos);
                  
      End;        
    If IsSold then  // Grid dinâmico quando está vendido
      Begin
        If Position >= -contratos then
          if (Close[1] >= n1) ou (Close[1] <= n1) then SellShortLimit(n2, Contratos);
        If Position >= -(contratos * 2) then
          if (Close >= n2) then SellShortLimit(n3, Contratos);
        If Position >= -(contratos * 3) then
          if (Close >= n3) then SellShortLimit(n4, Contratos);
        If Position >= -(contratos * 4) then
          if (Close >= n4) then SellShortLimit(n5, Contratos);
          If Position >= -(contratos * 5) then
          if (Close >= n5) then SellShortLimit(n6, Contratos);
          If Position >= -(contratos * 6) then
          if (Close >= n6) then SellShortLimit(n7, Contratos);
          If Position >= -(contratos * 7) then
          if (Close >= n7) then SellShortLimit(n8, Contratos);
          If Position >= -(contratos * 8) then
          if (Close >= n8) then SellShortLimit(n9, Contratos);
          If Position >= -(contratos * 9) then
          if (Close >= n9) then SellShortLimit(n10, Contratos);
          If Position >= -(contratos * 10) then
          if (Close >= n10) then SellShortLimit(n11, Contratos);
          If Position >= -(contratos * 11) then
          if (Close >= n11) then SellShortLimit(n12, Contratos);
          If Position >= -(contratos * 12) then
          if (Close >= n12) then SellShortLimit(n13, Contratos);
          If Position >= -(contratos * 13) then
          if (Close >= n13) then SellShortLimit(n14, Contratos);
          If Position >= -(contratos * 14) then
          if (Close >= n14) then SellShortLimit(n15, Contratos);
          If Position >= -(contratos * 15) then
          if (Close >= n15) then SellShortLimit(n16, Contratos);
          If Position >= -(contratos * 16) then
          if (Close >= n16) then SellShortLimit(n17, Contratos);
          If Position >= -(contratos * 17) then
          if (Close >= n17) then SellShortLimit(n18, Contratos);
          If Position >= -(contratos * 18) then
          if (Close >= n18) then SellShortLimit(n19, Contratos);
          If Position >= -(contratos * 19) then
          if (Close >= n19) then SellShortLimit(n20, Contratos);
          If Position >= -(contratos * 20) then
          if (Close >= n20) then SellShortLimit(n21, Contratos);
          If Position >= -(contratos * 21) then
          if (Close >= n21) then SellShortLimit(n22, Contratos);
          If Position >= -(contratos * 22) then
          if (Close >= n22) then SellShortLimit(n23, Contratos);
          If Position >= -(contratos * 23) then
          if (Close >= n23) then SellShortLimit(n24, Contratos);
          If Position >= -(contratos * 24) then
          if (Close >= n24) then SellShortLimit(n25, Contratos);
          If Position >= -(contratos * 25) then
          if (Close >= n25) then SellShortLimit(n26, Contratos);
          If Position >= -(contratos * 26) then
          if (Close >= n26) then SellShortLimit(n27, Contratos);
          If Position >= -(contratos * 27) then
          if (Close >= n27) then SellShortLimit(n28, Contratos);
          If Position >= -(contratos * 28) then
          if (Close >= n28) then SellShortLimit(n29, Contratos);
          If Position >= -(contratos * 29) then
          if (Close >= n29) then SellShortLimit(n30, Contratos);
          
      End;
  End;

//----------------------------------------------------------------------------------//
// Faz a montagem do grid completo de uma só vez assim que fica posicionado
//----------------------------------------------------------------------------------//

If not GridDinamico then
  Begin
  //-----------------------------------------------------------//
  // Montagem do Grid Completo com a utilização um Loop "for"  //
  //-----------------------------------------------------------// 
    Begin  // Inicio do bloco de código com loop for
    
    // Bloco de Compra
      If IsBought then
        Begin
          // Posicionamento Total da Ordem de Stop
          SellToCoverStop(n1 - (Stop * MinPriceIncrement), n1 - (Stop * MinPriceIncrement), Position);

          // Loop para montagem do Grid de ordens
          for i := (buyPosition) to 29 do
            Begin
              nGrid := n1 - ((DistanciaEntreNiveis * MinPriceIncrement) * i);
              If (Close > nGrid) then            
                BuyLimit(nGrid, Contratos);
            End;

          // Loop para posicionamento das ordens de saída do Grid
          for i := 0 to (BuyPosition + 1) do
            Begin
              nGrid := (n1 + (DistanciaEntreNiveis * MinPriceIncrement)) - (i * (DistanciaEntreNiveis * MinPriceIncrement));
              If (Close < nGrid) then            
                SellToCoverLimit(nGrid, Contratos);
            End;
        End;

    // Bloco de Venda
      If IsSold then
        Begin
          // Posicionamento Total da Ordem de Stop
          BuytoCoverStop(n1 + (Stop * MinPriceIncrement), n1 + (Stop * MinPriceIncrement), -Position);

          // Loop para montagem do Grid de ordens
          for i := (SellPosition) to 29 do
            Begin
              nGrid := n1 + ((DistanciaEntreNiveis * MinPriceIncrement) * i);
              If (Close < nGrid) then            
                SellShortLimit(nGrid, Contratos);
            End;

          // Loop para posicionamento das ordens de saída do Grid
          for i := 0 to (SellPosition - 1) do
            Begin
              nGrid := (n1 - (DistanciaEntreNiveis * MinPriceIncrement)) + (i * (DistanciaEntreNiveis * MinPriceIncrement));
              If (Close > nGrid) then            
                BuyToCoverLimit(nGrid, Contratos);
            End;
        End;
    End;
  End; // Fim do Bloco do Grid não Dinâmico
      

  // Bloco de teste de plotagem dos níveis para Debug//
{  for i := 1 to 6 do
    Begin           
      nGrid := Highest(high,200)[1] + (50 * i);
      plotn(i, nGrid);      
    End; 
}
  
 

End;
end;



end;



   



                                               

