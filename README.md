
recover=gg.getResults(100000)
function AppSearch(SSNR,XGNR,BCNR,notWrite)
  gg.clearResults()
  gg.setRanges(SSNR["M"])
  gg.searchNumber(SSNR[1]["mv"],SSNR[1]["lx"])
  jg=gg.getResults(100000)
  local base=(SSNR[1]["offs"] or 0)
  local data={}
  if #jg==0 then
   
    gg.loadResults(recover)
    return nil
  end
  for i=1,#jg do
    jg[i].Useful=true
  end
  
    for k=2,#SSNR do
      local content={}
      local offset=SSNR[k]["offs"]-base
      local value=SSNR[k]["sv"]
      local type=SSNR[k]["lx"]
      local to=(SSNR[k]["to"] or value)
      local num={}
      --gg.alert(offset..":"..value..":"..to)
      if to<value then
        to,value=value,to
      end
      
      --↓
      for i=1,#jg do
        if jg[i].Useful==true then
          table.insert(content,{})
          content[#content].address=jg[i].address+offset--偏移部分
          content[#content].flags=type
          num[#num+1]=i
        end
      end
      --存放偏移后的部分↑
      
      --↓
      if #content==0 then  gg.loadResults(recover) return nil end
      content=gg.getValues(content)
      --存放完一起gg.getValues↑
      
      --一起判断↓
      for i,v in pairs(content) do
        if tonumber(v.value)<tonumber(value) or tonumber(v.value)>tonumber(to) then
          jg[num[i]].Useful=false
        end
      end
      --↑
      
    end
    
    for j=1,#jg do
      if jg[j].Useful==true then
        data[#data+1]=jg[j].address
      end
    end
     
  if #data==0 then
   
    gg.loadResults(recover)
    return nil
  end
  if notWrite==true then
    gg.loadResults(recover)
    return data
  end
  if XGNR then
  local write={}
  for i=1,#data do
    for j=1,#XGNR do
      write[#write+1]={}
      write[#write].address=data[i]+(XGNR[j][2]-base)
      write[#write].flags=XGNR[j][3]
      write[#write].value=XGNR[j][1]
      write[#write].freeze=XGNR[j][4]
      write[#write].name=XGNR[j][5] or nil
      if write[#write].freeze==true then
        gg.addListItems({[1]=write[#write]})
      else
        gg.setValues({[1]=write[#write]})
      end
      if XGNR[j][6]==true then
        gg.addListItems({[1]=write[#write]})
      end
    end
  end
  end
  if BCNR then
  local bc={}
  for j=1,#data do
  for i=1,#BCNR do
    bc[#bc+1]={}
    bc[#bc].address=data[j]+(BCNR[i][1]-base)
    bc[#bc].flags=BCNR[i][2]
    bc[#bc].name=BCNR[i][3]
  end
  end
  gg.addListItems(bc)
  end
  gg.toast("修改成功")
  gg.loadResults(recover)
end


function main()
  FX=0
  local main=gg.choice({'1.『 手机  』','2.『 电脑  』'},nil,'选择运行的设备')
  if main== 1 then TU=0 main1() end
  if main== 2 then TU=1 main1() end
  if main== nil then  end end
  
  
  
  
function main1()
  FX=1
  if TU==1 then  top='不可用'  else top='注意开启锁血' end
  sn=gg.multiChoice({"『1.人物锁血』","『2.部分人物秒杀』","『3.自动秒怪』"..top,"『4.游戏加速』","『5.清除冻结数据』","『6.退出脚本』"},nil,"ㄨ请勿用于刷排行榜ㄨ\nㄨ以下功能除加速以外均在游戏副本内打开ㄨ\nㄨ锁血不要和小怪战斗的时候打开ㄨ")
  if sn==nil then else
    if sn[1]==true then SN1() end
    if sn[2]==true then SN2() end
    if sn[3]==true then SN3() end
    if sn[4]==true then SN4() end
    if sn[5]==true then SN5() end
    if sn[6]==true then gg.clearList() gg.clearResults() os.exit() end
  end
end

function SN1()
gg.setRanges(32)
gg.clearResults()
if TU==1 then SN1_1() goto  Label  end

ss={
["M"]=32,
{["mv"]="-458752",["lx"]=32},
{["sv"]="-1970324836974592",["offs"]=-0xc,["lx"]=32},
{["sv"]="1077936128",["to"]="1086324736",["offs"]=-0x10,["lx"]=4}
}
xg={
{10,-0x10,16,true}
}
AppSearch(ss,xg)
:: Label ::
end

function SN1_1()
gg.setRanges(gg.REGION_ANONYMOUS)
  gg.searchNumber("59;-1;0;3F~6F;0;0;0;0;0;-1::41",gg.TYPE_DWORD)
  local count=gg.getResultCount()
  if count==0 then gg.toast("锁血开启失败") goto Label end

  gg.searchNumber("3F~6F",gg.TYPE_FLOAT)
  local count=gg.getResultCount()
  if count==0 then gg.toast("锁血开启失败") goto Label end

  local i=gg.getResultCount()
  i1=i
  local t=gg.getResults(i)
  while (i)
    do
    t[i].value='6'
    t[i].freeze=true
    i=i-1
    if i==0 then i=nil end
  end
  gg.addListItems(t)
  gg.toast("修改到"..count.."数据")
  gg.clearResults()
:: Label ::
end




function SN2()
array={}
array={1075838976,1076232192,1075052544,1076494336,1075970048}
for i=1,5,1 do
ss={
["M"]=32,
{["mv"]=array[i],["lx"]=32},
{["sv"]=-1,["lx"]=4,["offs"]=-0x8},
{["sv"]=2.5,["to"]=5,["lx"]=16,["offs"]=0x8}
}
xg={
{9,0x8,16,true}
}
AppSearch(ss,xg)
end

end
function SN3() 
gg.clearResults()
gg.setRanges(32)
gg.setVisible(false)
gg.toast('开始运行，再次点击暂停')
while (true) do
if gg.isVisible(true) then gg.toast('已中止') break end

ss={
["M"]=32,
{["mv"]="-458752",["lx"]=32},
{["sv"]="-1970324836974592",["offs"]=-0xc,["lx"]=32},
{["sv"]="1077936128",["to"]="1086324736",["offs"]=-0x10,["lx"]=4}
}
xg={
{0,-0x10,16}
}
AppSearch(ss,xg)
             end
                        
end


function SN4()
  gg.clearResults()
  gg.setRanges(4)
  local sn=gg.choice({'2倍数','3倍数','4倍数','6倍数','倍数恢复'})
  local sn_1
  if sn==1 then sn_1=1073741824 end
  if sn==2 then sn_1=1077936128 end
  if sn==3 then sn_1=1082130432 end
  if sn==4 then sn_1=1086324736 end
  if sn==5 then sn_1=1065353216 end
  if sn== nil then  goto Label end

  if tep16~=nil then gg.searchAddress(tep16,FFFFFFFF,4)
    toc=gg.getResults(1)
    if sn==5 then
      toc[1].value=sn_1
      toc[1].freeze=true
       gg.addListItems(toc) gg.toast('恢复成功') goto Label
     else
      toc[1].value=sn_1
      toc[1].freeze=true
      gg.addListItems(toc) gg.toast('开启成功') goto Label end

  end

  gg.searchNumber('1065353216;1051372203;1022739087::9',4)
  local count=gg.getResultCount()
  if count==0 then gg.toast('开启失败') goto Label end

  gg.searchNumber('1065353216')
  local count=gg.getResultCount()
  if count==0 then gg.toast('开启失败') goto Label end
  gg.getResults(1)
  local soc = gg.getResults(1)
  soc[1].value=sn_1
  soc[1].freeze=true
  gg.addListItems(soc)
  gg.toast('开启加速')
  tep16=string.format("%#x",soc[1].address)
::Label::

end


function SN5()
  gg.clearList()
  gg.clearResults()
  gg.toast("执行成功")
end


while true do
  if gg.isVisible(true) then
    if FX==nil then FX=nil else if FX==0 then FX=nil end end
    if FX==1 then FX=2 end
    if FX==3 then FX=4 end

    gg.setVisible(false)
  end
  if FX == nil then main() end
  if FX == 2 then main1() end
end


