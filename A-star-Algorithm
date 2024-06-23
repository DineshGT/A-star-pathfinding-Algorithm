console.log("Hello from A*");

//heuristic function 
function heuristic(val1, val2)
{
  var distance = abs(val1.i-val2.i)+ abs(val1.j-val2.j);
  return distance;
}
//Global variables..
var rows = 40;
var cols = 40;
var grid = new Array(rows);

var openlist =[];
var closedlist = [];
var start;
var end;
var w,h;
var current;
var nosolution = false;





//inside nodes
function nodes (i,j)
{
  this.i = i;
  this.j = j;
  this.f=0;
  this.g=0;
  this.h=0;
  this.neighbours = [];
  this.previous = undefined;
  this.walls = false;
  
  // creating random walls
  if(random(1)<0.3)
    {
      this.walls = true;
    }
  
  this.show = function(col)
  {
    fill(col);
    if(this.walls)
      {
        fill(0);
      }
    noStroke();
    rect(this.i * w, this.j * h, w-1,h-1);
  }
  
  this.addneighbours = function(grid)
  {
    var i = this.i;
    var j = this.j;
     if(i<cols-1)
      {
        this.neighbours.push(grid[i+1][j]);
      }
     if(i>0)
      {
        this.neighbours.push(grid[i-1][j]);
      }
     if(j<rows-1)
      {
        this.neighbours.push(grid[i][j+1]);
      }
     if(j>0)
      {
        this.neighbours.push(grid[i][j-1]);
      }
//     if(i>0 && j>0)
//       {
//                 this.neighbours.push(grid[i-1][j-1]);
//       }
//     if(i<cols-1 && j>0)
//       {
//                 this.neighbours.push(grid[i+1][j-1]);
//       }
//     if(i>0 && j<rows-1)
//       {
//                 this.neighbours.push(grid[i-1][j+1]);
//       }
//     if(i<cols-1 && j<rows-1)
//       {        this.neighbours.push(grid[i+1][j+1]);
        
//       }
    
  }
  
}





function setup() {
  console.log("helolo");
  createCanvas(500, 500);
  w = width /cols;
  h = height /rows;
  //creating a 2d grid
  for(var i=0;i<rows;i++)
    {
      grid[i] = new Array(cols);
    }

  for(var i=0; i<rows; i++)
    {
      for(var j=0; j<cols; j++)
        {
          grid[i][j] = new nodes(i, j);
        }
    }

  for(var i=0; i<cols; i++)
    {
      for(var j=0; j<rows; j++)
        {
          grid[i][j].addneighbours(grid);
        }
    }

  start = grid[0][0];
  end = grid[rows-1][cols-1];
  //destination should not be a wall
  start.walls = false;
  end.walls = false;

  openlist.push(start);
  console.log(grid);
}




function draw() {
  
      
  background(0);
  
  if(openlist.length > 0)
    {
      //finding route
      var winner = 0;
      for(var i=0;i<openlist.length;i++)
        {
          if(openlist[i].f<openlist[winner].f)
            {
              winner = i;
            }
        }
     var current = openlist[winner];

      //goal reached
      if(current === end)
        {
          noLoop();
          console.log("PATH FOUND!!!");

        }
      
      //func to remove 
      // remove_from_array(openlist, current);
       openlist.splice(winner,1);
      closedlist.push(current);
      
      
      var neighbours = current.neighbours;
      for(var i=0;i<neighbours.length;i++)
        {
          var neighbour = neighbours[i];
          //to add in the closed set if it was not present already
          if(!closedlist.includes(neighbour)&& neighbour.walls === false)
            {
              var tempg = current.g + 1;
              // console.log(neighbour.walls);
              // console.log(neighbour.i,neighbour.j);
              if(openlist.includes(neighbour))
                {
                  
                  if(tempg<neighbour.g)
                    {
                      //new g value
                      neighbour.g = tempg;
                    }
                }
              else
                {
                  neighbour.g = tempg;
                  openlist.push(neighbour);
                }
              
              
              //heuristic value..
              neighbour.h = heuristic(neighbour, end);
              neighbour.f = neighbour.g + neighbour.h;
              //track where we came from..
              neighbour.previous = current;
              
            }
          
        }
      
    }
  else
    {
      //no solution
      nosolution = true;
      noLoop();
      console.log("NO SOLUTION!");
    }
  
  for(var i=0;i<cols;i++)
    {
      for(var j=0;j<rows;j++)
        {
          grid[i][j].show(color(255));        }
    }
  
  for(var i=0;i<closedlist.length;i++)
    {
      closedlist[i].show(color(255, 0, 0));
    }
  
  for(var i=0;i<openlist.length;i++)
    {
      openlist[i].show(color(0, 255, 0));
    }
  if(!nosolution)
    {
  var path = [];
  var temp = current;
          path.push(temp);
          while(temp.previous)
            {
              path.push(temp.previous);
              temp = temp.previous;
            }
    }
  
  for(var i=0;i<path.length;i++)
    {
      path[i].show(color(0,0,255));
    }
  
}
