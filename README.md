### Learning Memory,Storage and Calldata

EVM can access and store information in the following places:<br>
1.Stack<br>
2.Memory<br>
3.Storage<br>
4.Calldata<br>
5.Code<br>
6.Logs<br>

From the above six we will focus on only Calldata,Memory and Storage.
```calldata``` and ```memory``` means that variables will only exist temporarily.<br>
```storage``` means that variables wil exits permanently.<br>
```calldata``` is temporary variable that can't be modified.<br>
```memory``` is temporary variable that can be modified<br>


So, here in the following code:

```
//SPDX-License-Identifier: MIT
pragma solidity ^0.8.7;

contract rafiSimplestorage {
  // basic data types: boolean, uint,int,address,bytes
  //uint(unsigned integer only positive),int both pos and neg
  //address is the address of the account
  //string are secretly byte objects only for text
  //bytes32 is a bytes objects whre 32 represent how many bytes we want them to be,max size is 32
  //byte objects look like 0xsdsysydggt
  //unint256 here 256 is bit (8,16,32 upto 256 we can use)
  uint256 goodNumber;//remove public so that we don't get duplicate functions at the moment we will just get the retrieve function
   //if we have whole bunch of variables inside the contract rafiSimplestorage those actually get indexed
   //here 'uint256 goodNumber' will get index to 'zero'
  
//Below we have created a new type in our solidity that holds both preferred number and name 
  struct People{
    uint256 goodNumber;//this get indexed to 0
    string name;// this get indexexd to 1
//whenever we have list of variables inside an object they automatically get indexed

}

  // here below we create an array of uint256 and now preferred number can be a list or array
  //uint256[] public goodNumbersList;

//here below we want an array of Individuals we give it visibility of public and variable name individuals
  People[] public people; //it is automatically giving a view function and it will give nothing if it is empty and in it's button the value that it wants is gonna be the index of the object
// array above is a dynamic array because size of the array is not given at it's initialization if we don't add any size it can be any size and here we gonna work with dynamic array

//pasing parameter of type uint256 and made the function public
  function store(uint256 _goodNumber) public{
      goodNumber = _goodNumber;
    
  }

  function retrieve() public view returns(uint256){
    return goodNumber;
  }

  //now we will create a function that is going to add individuals to Individual array
  function addCustomer(string memory _name, uint256 _goodNumber) public {
      
      people.push(People(_goodNumber,_name));//Here we have created a push function which is available in our People object
      // I have remove the semicolon from the above code 
      //Here in the above inside the push function we have created a new people object that will take good number and name. 
  //push People in our people array ,we can also do in this way
  }
  //We don't need the 'name' variable after the above function runs we can keep it as memory
  //We can also keep the name as 'calldata' in that case we can't modify it 


  
}

```

Here in ```function addCustomer(string memory _name, uint256 _goodNumber) public{}``` function ```_name``` variable will exist temporarily during transaction.<br>
Here in the above code ```uint256 goodNumber;``` is automatically a storage variable even though we don't specify it because it is not explictly defined in other functions which means that its scope is not clearly defined.<br>
Here in ```function addCitizen(string memory _name, uint256 _goodNumber) public {}``` if we use ```memory``` keyword before ```_preferredNumber``` the code will not be compiled<br>
Because solidity automatically knows ```uint256 _goodNumber``` will exists in memory, but does no know about ```string memory _name```<br>
Because ```string``` are actually kind of complicated .<br>
Since it is secretly an array of bytes we need to add this ```memory``` bit to it because we need to tell the solidity the data location of arrays,structs or mappings<br>
If we use ```storage```  before  ```_name``` in this function ```function addCustomer(string memory _name, uint256 _goodNumber) public {}``` it will also show errors <br>
because solidity knows that since ```function addCitizen(string memory _name, uint256 _goodNumber) public {}```  is a function<br>
```_name``` parameter of this function is not actually getting stored anywhere<br>
Struct,arrays and mapping needed to be given ```memory``` or ```calldata``` keyword when adding them as parameters of diferent functions.<br>

### Learning Basic Solidity Mappings

Mapping is just like a dictionary,it is a set of keys where each key returns values associated with that key.<br>
Here is an example code:<br>
```
//SPDX-License-Identifier: MIT
pragma solidity ^0.8.7;

contract akrkSimplestorage {
  // basic data types: boolean, uint,int,address,bytes
  //uint(unsigned integer only positive),int both pos and neg
  //address is the address of the account
  //string are secretly byte objects only for text
  //bytes32 is a bytes objects whre 32 represent how many bytes we want them to be,max size is 32
  //byte objects look like 0xsdsysydggt
  //unint256 here 256 is bit (8,16,32 upto 256 we can use)
  uint256 preferredNumber;//remove public so that we don't get duplicate functions at the moment we will just get the retrieve function
   //if we have whole bunch of variables inside the contract akrkSimplestorage those actually get indexed
   //here 'uint256 preferredNumber' will get index to 'zero'
//below is type mapping of 'string' to 'uint256', visibility is 'public'
   mapping(string => uint256) public nameToPreferredNumber;//Here we have kind of dictionary where we gonna map a specific name to a specific number
  //When we create mapping we initiaize everything to it's null value so every possible string is initialize to having preferredNumber to zero, for that we have to manually change it.
//Below we have created a new type in our solidity that holds both preferred number and name 
  struct Individuals{
    uint256 preferredNumber;//this get indexed to 0
    string name;// this get indexexd to 1
//whenever we have list of variables inside an object they automatically get indexed

}

  // here below we create an array of uint256 and now preferred number can be a list or array
  //uint256[] public preferredNumbersList;

//here below we want an array of Individuals we give it visibility of public and variable name individuals
  Individuals[] public individuals; //it is automatically giving a view function and it will give nothing if it is empty and in it's button the value that it wants is gonna be the index of the object
// array above is a dynamic array because size of the array is not given at it's initialization if we don't add any size it can be any size and here we gonna work with dynamic array

//pasing parameter of type uint256 and made the function public
  function store(uint256 _preferredNumber) public{
      preferredNumber = _preferredNumber;
    
  }

  function retrieve() public view returns(uint256){
    return preferredNumber;
  }

  //now we will create a function that is going to add individuals to Individual array
  function addCitizen(string memory _name, uint256 _preferredNumber) public {
      
      individuals.push(Individuals(_preferredNumber,_name));//Here we have created a push function which is available in our Individuals object
      nameToPreferredNumber[_name]=_preferredNumber ;//here we are going to add Individual to the individuals array where we add key name equal to preferred number
      // I have remove the semicolon from the above code 
      //Here in the above inside the push function we have created a new Individual object that will take preferred number and name. 
  //push Individual in our individual array ,we can also do in this way
  }
  //We don't need the 'name' variable after the above function runs we can keep it as memory
  //We can also keep the name as 'calldata' in that case we can't modify it 


  
}

//0xd9145CCE52D386f254917e481eB44e9943F39138
```
 We get following output,<br>
 
![bl1](https://user-images.githubusercontent.com/89090776/227698505-f7a0f968-9a04-4d3a-b8c1-bfa397a66881.jpg)
Figure1:Here in the above figure ,I have added manually ```Khatami,68```  , ```Rokib,53```,  ```Rafi,65``` in the form of orange color ```addPerson``` button<br>
Then when I typed one of the string suppose ```Khatami``` on the form of blue color ```nameToPrefer``` button then i will get desired prefferedNumber which is ```68``` of string ```Khatami```<br>

![bl3](https://user-images.githubusercontent.com/89090776/227699802-a59ccd28-465e-4435-8d16-6150b53255a0.jpg)
Figure2:In this Figure we can also those string assinged with eacfh preferredNumber in array when we typed each index at field of blue color ```individuals``` button<br>
because we kept them in this  ```individuals.push(Individuals(_preferredNumber,_name));``` function







