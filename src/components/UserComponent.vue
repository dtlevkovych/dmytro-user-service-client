<script>
export default {
  data: function() {
      return {
          users: []
      }
  },
  methods: {
    async getUsers() {
        console.log("1");
          try {
            console.log("2");
            const response =  await fetch("http://127.0.0.1:5000/users?order_by=id", {
                method: "GET",
                headers: {
                    "Content-Type": "application/json",
                }
            });
            console.log("3");
            const result = await response.json();
            console.log(result);
            
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
        console.log("1");
          try {
            console.log("2");
            const response =  await fetch("http://127.0.0.1:5000/user/" + userId, {
                method: "DELETE",
                headers: {
                    "Content-Type": "application/json",
                }
            });
            console.log("3");
            const result = await response.json();
            console.log(result);
            
            if (result.status == true) {
                this.getUsers();
            } else {
                alert(result.error_msg);
            }
        
        } catch (error) {
            alert("Error: ", error);
        }
     }
  }
}
</script>

<template>
    <article id="article-user" class="article-params">
        <button @click="getUsers">Refresh</button>
        <table style="text-align: left;">
            <tr v-for="u in users">
                <td>{{ u.firstName }}</td>
                <td>{{ u.lastName }}</td>
                <td>{{ u.age }}</td>
                <td><button @click="deleteUser(u.id)">Delete</button></td>
            </tr>
        </table>
    </article>
</template>