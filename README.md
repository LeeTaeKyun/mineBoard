# 지뢰찾기 관련 로직입니다.

``` javascript
const rowAll = 10;
const colAll = 10;
const mineAll = 10;

let mineBoard = [];

function init(){
	mineBoard = [];

	for(let i=0; i<rowAll; i++){

		mineBoard[i] = [];

		for(let j=0; j<colAll; j++){

			mineBoard[i][j] = 0;
		}		
	}

	setBoom(mineAll);
}

function setBoom(cnt = 10){

	for(let i=0; i<cnt; i++){

		let sq1 = Math.floor(Math.random() * 9);
		let sq2 = Math.floor(Math.random() * 9);
    
		if(mineBoard[sq1][sq2] === 1)
			i--;
		else
			mineBoard[sq1][sq2] = '*';
	
  }
}

function getMineCount(row, col){

	let mineCnt = 0;
  
	if(isMine(row-1, col-1))mineCnt++;
	if(isMine(row-1, col))mineCnt++;
	if(isMine(row-1, col+1))mineCnt++;
	if(isMine(row, col-1))mineCnt++;
	if(isMine(row, col+1))mineCnt++;
	if(isMine(row+1, col-1))mineCnt++;
	if(isMine(row+1, col))mineCnt++;
	if(isMine(row+1, col+1))mineCnt++;

    return mineCnt;
}

function isMine(row, col){

	if(row >= 0 && row < rowAll && col >= 0 && col < colAll)
	   return ( mineBoard[row][col] === '*')? true : false;
}

function start(){

    init();
    console.log('----------------지뢰찾기----------------');
    console.log('ROW : '+rowAll);
    console.log('COL : '+colAll);

	for(let i=0; i<mineBoard.length; i++){
  
		for(let j=0; j<mineBoard[i].length; j++){
    
		    let cnt = 0;
		    cnt = getMineCount(i, j);

			if(mineBoard[i][j] !== '*'){
      
				mineBoard[i][j] = cnt;
              
			}else{

        mineBoard[i][j] = '(*)'+cnt;
			}
		}
	}
  
	console.table(mineBoard);
}
start();
```

