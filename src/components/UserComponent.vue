<script>
export default {
  data: function() {
      return {
          users: []
      }
  },
  methods: {
    refresh() {
        this.showUserTable();
        this.getUsers();
    },
    async getUsers() {
          try {
            const response =  await fetch("http://127.0.0.1:5000/users?order_by=id", {
                method: "GET",
                headers: {
                    "Content-Type": "application/json",
                }
            });
            const result = await response.json();
            
            if (result.status == true) {
                this.users = [];
                for(var i = 0; i < result.data.length; i++) {
                    this.users.push(result.data[i]);
                }
            } else {
                alert(result.error_msg);
            }
        
        } catch (error) {
            alert("Error: ", error);
        }
     },
     async deleteUser(userId) {
          try {
            const response =  await fetch("http://127.0.0.1:5000/user/" + userId, {
                method: "DELETE",
                headers: {
                    "Content-Type": "application/json",
                }
            });
            const result = await response.json();
            
            if (result.status == true) {
                this.getUsers();
            } else {
                alert(result.error_msg);
            }
        
        } catch (error) {
            alert("Error: ", error);
        }
     },
     showUserTable() {
        document.getElementById("user-table").style.display = "block";
        document.getElementById("user-edit").style.display = "none";
     },
     showAddUser() {
        document.getElementById("user-table").style.display = "none";
        document.getElementById("user-edit").style.display = "block";
     },
     showUpdateUser() {
        document.getElementById("user-table").style.display = "none";
        document.getElementById("user-edit").style.display = "block";
     },
     async addUser() {
        var firstName = document.getElementById("firstName").value;
        var lastName = document.getElementById("lastName").value;
        var age = document.getElementById("age").value;
        var obj = {
            firstName: firstName,
            lastName: lastName,
            age: age
        };
        try {
            const response =  await fetch("http://127.0.0.1:5000/user", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                },
                body: JSON.stringify(obj)
            });
            const result = await response.json();

            if (result.status == true) {
                this.refresh();
            } else {
                alert(result.error_msg);
            }

        } catch (error) {
            alert("Error: ", error);
        }
    }
},
  mounted() {
    this.refresh();
  }
}
</script>

<template>
    <article id="article-user" class="article-params">
    <div id="user-table" style="text-align: center;">
        <table class="table">
            <thead class="thead-dark">
                <tr>
                    <th scope="col">First Name</th>
                    <th scope="col">Last Name</th>
                    <th scope="col">age</th>
                    <th scope="col"><button @click="showAddUser()" class="btn btn-outline-success btn-sm">Add</button></th>
                </tr>
            </thead>
            <tr v-for="u in users">
                <td>{{ u.firstName }}</td>
                <td>{{ u.lastName }}</td>
                <td>{{ u.age }}</td>
                <td><button @click="deleteUser(u.id)" class="btn btn-outline-danger btn-sm">Delete</button></td>
            </tr>
        </table>
    </div>
    <div id="user-edit">
        <form>
            <div class="control-group mx-auto m-3 w-25">
                <label for="firstName">First name</label>
                <input id="firstName" type="text" class="form-control">
            </div>

            <div class="control-group mx-auto m-3 w-25">
                <label for="lastName">Last name</label>
                <input id="lastName" type="text" class="form-control">
            </div>

            <div class="control-group mx-auto m-3 w-25">
                <label for="age">Age</label>
                <input id="age" type="number" class="form-control">
            </div>

            <div class="control-group mx-auto m-3 w-25">
                <button @click="addUser()" class="btn btn-outline-success btn-sm">Save</button>
                &nbsp;
                <button @click="showUserTable()" class="btn btn-outline-dark btn-sm">Cancel</button>
            </div>
        </form>
    </div>
    </article>
</template>