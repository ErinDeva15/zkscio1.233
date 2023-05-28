# zkscio1.233
// 查询 ETH 等原生资产余额
function getEthBalance(walletAddress, network) {
  let rpcLink = RPC_MAP[network];
  if (!rpcLink) {
    return "Error: Invalid Network Name";
  }
  const data = "0x" + "balanceOf" + "000000000000000000000000" + walletAddress.slice(2);
  const response = UrlFetchApp.fetch(rpcLink, {
    method: "post",
    payload: JSON.stringify({
      "jsonrpc": "2.0",
      "method": "eth_getBalance",
      "params": [walletAddress, "latest"],
      "id": 1
    }),
    contentType: "application/json",
    muteHttpExceptions: true
  });
  let result = JSON.parse(response.getContentText());
