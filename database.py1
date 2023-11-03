import motor.motor_asyncio

class Database:
    def __init__(self, url, database_name):
        self._client = motor.motor_asyncio.AsyncIOMotorClient(url)
        self.db = self._client[database_name]
        self.col = self.db.users

    def new_user(self, user_id):
        return dict(id=user_id)

    async def add_user(self, user_id):
        user = self.new_user(user_id)
        try:
            await self.col.insert_one(user)
        except Exception as e:
            print(f"Error adding user: {e}")

    async def is_user_exist(self, user_id):
        try:
            user = await self.col.find_one({'id': int(user_id)})
            return user is not None
        except Exception as e:
            print(f"Error checking user existence: {e}")
            return False

    async def total_users_count(self):
        try:
            count = await self.col.count_documents({})
            return count
        except Exception as e:
            print(f"Error getting total users count: {e}")
            return 0

    async def get_all_users(self):
        try:
            all_users = self.col.find({})
            return all_users
        except Exception as e:
            print(f"Error getting all users: {e}")
            return []

    async def delete_user(self, user_id):
        try:
            await self.col.delete_many({'id': int(user_id)})
        except Exception as e:
            print(f"Error deleting user: {e}")
