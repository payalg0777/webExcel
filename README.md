#Youtube WorkFlows

1. Logging In - Simple
  * Data gathering requirements
    - User authentication data (username, password).
    - timestamp
    - IP address and device information for security purposes.

  * Edges and Nodes
    * Nodes
      - User (contains username, email, etc.).
      - Session (contains login timestamp, IP address, device info).
    * Edges
      - Relationship between User and Session (login session details)

  * SDL, Query, Mutation

  	  type User {
    	  id: ID!
    	  username: String!
    	  email: String!
    	  sessions: [Session]
    	}
  
    	type Session {
    	  id: ID!
    	  timestamp: String!
    	  ipAddress: String!
    	  deviceInfo: String!
    	}
    
    	type Query {
    	  getUser(id: ID!): User
    	  getSession(id: ID!): Session
    	}
    
    	type Mutation {
    	  loginUser(username: String!, password: String!, ipAddress: String!, deviceInfo: 	String!): Session
    	}


#############

2. Searching for Videos - Simple
  * Data gathering requirements
    - Search query entered by the user.
    - IP address and device information for search history.

  * Edges and Nodes
    * Nodes:
      - User
      - Search query
      - Device (contains device information).
    * Edges:
      - Relationship between User and SearchQuery (user's search history).
      - Relationship between User and Device (device used for search).

  * SDL, Query, Mutation 

     type SearchQuery {
    	  id: ID!
    	  text: String!
    	  timestamp: String!
    	}
    
    	type Device {
    	  id: ID!
    	  name: String!
    	  type: String!
    	}
    
    	type Query {
    	  getSearchQuery(id: ID!): SearchQuery
    	  getDevice(id: ID!): Device
    	}
    
    	type Mutation {
    	  searchVideos(userId: ID!, searchText: String!, timestamp: String!, deviceId: ID!): SearchQuery
    	}

#############

3. Uploading a Video - Complex
  * Data gathering requirements
    - Video file
    - Metadata (title, description, tags)
    - Privacy settings (public, unlisted, private).
    - Timestamp of upload.
    - IP address and device information for upload history.

  * Edges and Nodes
    * Nodes:
      - User
      - Video (metadata like title, description).
      - Upload (contains timestamp, upload status).
      - Device
    * Edges:
      - Relationship between User and Video (user uploaded the video).
      - Relationship between User and Upload (upload history).
      - Relationship between User and Device (device used for upload).

  * SDL, Query, Mutation

    type Video {
    	  id: ID!
    	  title: String!
    	  description: String!
    	  tags: [String!]!
    	  privacy: String!
    	  timestamp: String!
    	}
    
    	type Upload {
    	  id: ID!
    	  userId: ID!
    	  videoId: ID!
    	  timestamp: String!
    	}
    
    	type Mutation {
    	  uploadVideo(userId: ID!, videoId: ID!, title: String!, description: String!, tags: 		[String!]!, privacy: String!, timestamp: String!): Upload
    	}
    	

#############

4. Managing Playlists - Complex
  * Data gathering requirements
    - Playlist titles and descriptions.
    - Videos added to playlists.
    - Privacy settings (public, unlisted, private) of playlists.
    - Timestamps of playlist creation and modifications.

  * Edges and Nodes
    * Nodes:
      - User
      - Playlist (contains title, description).
      - Video
    * Edges:
      - Relationship between User and Playlist (user's playlists).
      - Relationship between Playlist and Video (videos included in the playlist).

  * SDL, Query, Mutation

    type Playlist {
    	  id: ID!
    	  title: String!
    	  description: String!
    	  videos: [Video]
    	}
    
    	type Mutation {
    	  createPlaylist(userId: ID!, title: String!, description: String!): Playlist
    	  addVideoToPlaylist(userId: ID!, playlistId: ID!, videoId: ID!): Playlist
    	}

