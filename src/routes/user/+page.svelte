<script lang="ts">
    import { onMount } from 'svelte';
    
    // Sample data for the channels and messages
    const channels = [
      { id: 1, name: 'Announcements', unread: 2, category: 'Information' },
      { id: 2, name: 'Info', unread: 0, category: 'Information' },
      { id: 3, name: 'FAQ', unread: 0, category: 'Information' },
      { id: 4, name: 'Rules', unread: 0, category: 'Information' },
      { id: 5, name: 'Feedback', unread: 10, category: 'Channels' },
      { id: 6, name: 'User Interface', unread: 0, category: 'Channels' },
      { id: 7, name: 'User Experience', unread: 0, category: 'Channels' },
      { id: 8, name: 'Development', unread: 0, category: 'Channels' },
      { id: 9, name: 'Events', unread: 0, category: 'Channels' },
      { id: 10, name: 'Meetings', unread: 15, category: 'Channels' },
      { id: 11, name: "Steve's Dungeon", unread: 3, category: 'Private Channels' },
      { id: 12, name: 'Destiny 2', unread: 0, category: 'Private Channels' },
      { id: 13, name: 'Dubstep', unread: 0, category: 'Private Channels' },
      { id: 14, name: 'Drum and Bass', unread: 5, category: 'Private Channels' },
    ];
  
    const messages = [
      {
        id: 1,
        user: { name: 'Suyog Tandel', avatar: 'user (1).jpeg' },
        content: 'Do you know what could beat the exciting feeling of having a new computer? Make yours new PC!',
        timestamp: '14:53',
        attachments: ['attachments/image1.jpg']
      },
      {
        id: 2,
        user: { name: 'Krishnan H.', avatar: 'user (2).jpeg' },
        content: 'Crazy computer!',
        timestamp: '13:49'
      },
      {
        id: 3,
        user: { name: 'Soham Mayekar', avatar: 'user (3).jpeg' },
        content: 'Have you ever known exactly what you want to cook but searched and scrolled through all of your cookbook books.',
        timestamp: '13:10'
      },
      {
        id: 4,
        user: { name: 'Werda Wasey', avatar: 'user (4).jpeg' },
        content: 'In today\'s tech-savvy world it has become common for any business.',
        timestamp: '13:17'
      },
      {
        id: 5,
        user: { name: 'Hrishikesh Kumbhar', avatar: 'user (5).jpeg' },
        content: 'Chat is this real?',
        timestamp: '13:16'
      },
      {
        id: 6,
        user: { name: 'Aditya Suryavanshi', avatar: 'user (1).jpeg' },
        content: 'Less gooo.',
        timestamp: '13:07'
      }
    ];
  
    const users = [
      { id: 1, name: 'Krishnan H.', avatar: 'user (2).jpeg', status: 'online', role: 'admin' },
      { id: 2, name: 'Suyog Tandel', avatar: 'user (1).jpeg', status: 'online', role: 'admin' },
      { id: 3, name: 'Hrishikesh Kumbhar', avatar: 'user (5).jpeg', status: 'online', role: 'mod' },
      { id: 4, name: 'Werda Wasey', avatar: 'user (4).jpeg', status: 'idle', role: 'mod' },
      { id: 5, name: 'Soham Mayekar', avatar: 'user (1).jpeg', status: 'dnd', role: 'mod' },
      { id: 6, name: 'Viraj Pradhan', avatar: 'user (1).jpeg', status: 'offline', role: 'mod' },
      { id: 7, name: 'Arpita Yeligeti', avatar: 'user (1).jpeg', status: 'online', role: 'player' },
      { id: 8, name: 'Gauransh', avatar: 'user (1).jpeg', status: 'online', role: 'player' },
      { id: 9, name: 'Akshay N.', avatar: 'user (1).jpeg', status: 'idle', role: 'player' },
      { id: 10, name: 'Sujal Shetty', avatar: 'user (1).jpeg', status: 'dnd', role: 'player' },
      { id: 11, name: 'Shail Singh', avatar: 'user (1).jpeg', status: 'online', role: 'player' },
      { id: 12, name: 'Mayuresh', avatar: 'user (1).jpeg', status: 'online', role: 'player' },
      { id: 13, name: 'Dhriti', avatar: 'user (1).jpeg', status: 'offline', role: 'player' },
      { id: 14, name: 'Shaunak', avatar: 'user (1).jpeg', status: 'offline', role: 'afk' },
      { id: 15, name: 'Nishant', avatar: 'user (1).jpeg', status: 'offline', role: 'afk' }
    ];
  
    let activeChannel = 5; // Feedback channel is active by default
    
    onMount(() => {
      // Any initialization logic can go here
    });
  </script>
  
  <div class="app-container">
    <!-- Server sidebar -->
    <div class="server-sidebar">
      <div class="server-icon active">
        <img src="circuit_chat_icon.svg" alt="Circuit Chat" />
      </div>
      <div class="server-divider"></div>
      
      <!-- Sample server icons, replace with actual data -->
      <div class="server-icon"><span>WS</span></div>
      <div class="server-icon"><span>IN</span></div>
      <div class="server-icon"><span>DE</span></div>
      <div class="server-icon unread"><span>MT</span></div>
      <div class="server-icon"><span>PC</span></div>
      
      <div class="server-icon add-server">
        <span>+</span>
      </div>
      <div class="server-icon explore">
        <span>🔍</span>
      </div>
      
      <div class="user-controls">
        <div class="user-avatar">
          <img src="user(1).jpeg" alt="User Avatar" />
        </div>
      </div>
    </div>
  
    <!-- Channel sidebar -->
    <div class="channel-sidebar">
      <div class="server-header">
        <h2>Circuit Chat</h2>
        <button class="server-settings">⚙️</button>
      </div>
      
      <!-- Channel categories and channels -->
      <div class="channels-container">
        {#each ['Information', 'Channels', 'Private Channels'] as category}
          <div class="channel-category">
            <div class="category-header">
              <span class="category-arrow">▼</span>
              <h3>{category}</h3>
            </div>
            
            <div class="category-channels">
              {#each channels.filter(channel => channel.category === category) as channel}
                <div class="channel-item {activeChannel === channel.id ? 'active' : ''}">
                  <span class="channel-icon">#</span>
                  <span class="channel-name">{channel.name}</span>
                  {#if channel.unread > 0}
                    <span class="unread-badge">{channel.unread}</span>
                  {/if}
                </div>
              {/each}
            </div>
          </div>
        {/each}
      </div>
      
      <div class="user-panel">
        <div class="user-info">
          <div class="user-avatar-small">
            <img src="user(1).jpeg" alt="Your avatar" />
            <span class="status-indicator online"></span>
          </div>
          <div class="user-name-container">
            <span class="username">DXNTY</span>
            <span class="user-tag">#0401</span>
          </div>
        </div>
        <div class="user-controls">
          <button class="control-button">🎤</button>
          <button class="control-button">🎧</button>
          <button class="control-button">⚙️</button>
        </div>
      </div>
    </div>
  
    <!-- Main content area -->
    <div class="main-content">
      <!-- Channel header -->
      <div class="channel-header">
        <div class="channel-info">
          <span class="channel-icon">#</span>
          <h2>Feedback</h2>
        </div>
        <div class="channel-actions">
          <button class="action-button">🧵 6 unread messages</button>
          <div class="search-container">
            <input type="text" placeholder="Search" />
            <button class="search-button">🔍</button>
          </div>
        </div>
      </div>
  
      <!-- Message area -->
      <div class="message-area">
        {#each messages as message}
          <div class="message">
            <div class="message-avatar">
              <img src={message.user.avatar} alt={message.user.name} />
            </div>
            <div class="message-content">
              <div class="message-header">
                <span class="message-author">{message.user.name}</span>
                <span class="message-time">{message.timestamp}</span>
              </div>
              <div class="message-text">{message.content}</div>
              {#if message.attachments && message.attachments.length > 0}
                <div class="message-attachments">
                  {#each message.attachments as attachment}
                    <img src={attachment} alt="Attachment" class="message-attachment" />
                  {/each}
                </div>
              {/if}
            </div>
          </div>
        {/each}
      </div>
  
      <!-- Message input -->
      <div class="message-input-container">
        <div class="message-input-wrapper">
          <input type="text" placeholder="Type something..." class="message-input" />
          <button class="send-button">➡️</button>
        </div>
      </div>
    </div>
  
    <!-- Users sidebar -->
    <div class="users-sidebar">
      <div class="users-container">
        <!-- Admin users -->
        <div class="user-category">
          <h3>Admins - {users.filter(u => u.role === 'admin').length}</h3>
          {#each users.filter(u => u.role === 'admin') as user}
            <div class="user-item">
              <div class="user-avatar-small">
                <img src={user.avatar} alt={user.name} />
                <span class="status-indicator {user.status}"></span>
              </div>
              <span class="user-name">{user.name}</span>
            </div>
          {/each}
        </div>
  
        <!-- Mod users -->
        <div class="user-category">
          <h3>Mod - {users.filter(u => u.role === 'mod').length}</h3>
          {#each users.filter(u => u.role === 'mod') as user}
            <div class="user-item">
              <div class="user-avatar-small">
                <img src={user.avatar} alt={user.name} />
                <span class="status-indicator {user.status}"></span>
              </div>
              <span class="user-name">{user.name}</span>
            </div>
          {/each}
        </div>
  
        <!-- Players -->
        <div class="user-category">
          <h3>Players - {users.filter(u => u.role === 'player').length}</h3>
          {#each users.filter(u => u.role === 'player') as user}
            <div class="user-item">
              <div class="user-avatar-small">
                <img src={user.avatar} alt={user.name} />
                <span class="status-indicator {user.status}"></span>
              </div>
              <span class="user-name">{user.name}</span>
            </div>
          {/each}
        </div>
  
        <!-- AFK users -->
        <div class="user-category">
          <h3>AFK - {users.filter(u => u.role === 'afk').length}</h3>
          {#each users.filter(u => u.role === 'afk') as user}
            <div class="user-item">
              <div class="user-avatar-small">
                <img src={user.avatar} alt={user.name} />
                <span class="status-indicator {user.status}"></span>
              </div>
              <span class="user-name">{user.name}</span>
            </div>
          {/each}
        </div>
      </div>
    </div>
  </div>
  
  <style>
    /* Base styles */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Poppins', sans-serif;
    }
    
    :global(body) {
      background-color: #1e1e2e; /* Catppuccin Mocha base */
      color: #cdd6f4; /* Catppuccin Text */
      height: 100vh;
      overflow: hidden;
    }
    
    .app-container {
      display: grid;
      grid-template-columns: 70px 240px 1fr 240px;
      height: 100vh;
    }
    
    /* Server sidebar */
    .server-sidebar {
      background-color: #11111b; /* Catppuccin Crust */
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 10px 0;
      gap: 8px;
      overflow-y: auto;
    }
    
    .server-icon {
      width: 50px;
      height: 50px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      background-color: #313244; /* Catppuccin Surface0 */
      color: #cdd6f4; /* Catppuccin Text */
      font-weight: bold;
      cursor: pointer;
      transition: all 0.2s ease;
      position: relative;
    }
    
    .server-icon img {
      width: 32px;
      height: 32px;
    }
    
    .server-icon.active {
      background-color: #cba6f7; /* Catppuccin Mauve */
      border-radius: 16px;
    }
    
    .server-icon.active::before {
      content: "";
      position: absolute;
      width: 4px;
      height: 40px;
      background-color: white;
      border-radius: 0 2px 2px 0;
      left: -10px;
    }
    
    .server-icon.unread::after {
      content: "";
      position: absolute;
      width: 8px;
      height: 8px;
      background-color: #f5c2e7; /* Catppuccin Pink */
      border-radius: 50%;
      bottom: 0;
      right: 0;
    }
    
    .server-icon:hover {
      background-color: #cba6f7; /* Catppuccin Mauve */
      border-radius: 16px;
    }
    
    .server-divider {
      width: 30px;
      height: 2px;
      background-color: #313244; /* Catppuccin Surface0 */
      margin: 4px 0;
    }
    
    .add-server {
      background-color: #313244; /* Catppuccin Surface0 */
      color: #a6e3a1; /* Catppuccin Green */
      font-size: 24px;
    }
    
    .explore {
      background-color: #313244; /* Catppuccin Surface0 */
      font-size: 20px;
    }
    
    .user-controls {
      margin-top: auto;
    }
    
    .user-avatar {
      width: 50px;
      height: 50px;
      border-radius: 50%;
      overflow: hidden;
    }
    
    .user-avatar img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }
    
    /* Channel sidebar */
    .channel-sidebar {
      background-color: #181825; /* Catppuccin Mantle */
      display: flex;
      flex-direction: column;
      border-right: 1px solid #313244; /* Catppuccin Surface0 */
    }
    
    .server-header {
      padding: 16px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-bottom: 1px solid #313244; /* Catppuccin Surface0 */
    }
    
    .server-header h2 {
      color: #cdd6f4; /* Catppuccin Text */
      font-size: 16px;
      font-weight: 600;
    }
    
    .server-settings {
      background: none;
      border: none;
      color: #a6adc8; /* Catppuccin Subtext0 */
      cursor: pointer;
      font-size: 16px;
    }
    
    .channels-container {
      flex: 1;
      overflow-y: auto;
      padding: 8px 0;
    }
    
    .channel-category {
      margin-bottom: 16px;
    }
    
    .category-header {
      padding: 0 16px;
      display: flex;
      align-items: center;
      gap: 4px;
      cursor: pointer;
      margin-bottom: 4px;
    }
    
    .category-arrow {
      font-size: 10px;
      color: #a6adc8; /* Catppuccin Subtext0 */
    }
    
    .category-header h3 {
      color: #a6adc8; /* Catppuccin Subtext0 */
      font-size: 12px;
      font-weight: 600;
      text-transform: uppercase;
    }
    
    .channel-item {
      padding: 6px 8px 6px 20px;
      margin: 1px 8px;
      display: flex;
      align-items: center;
      gap: 6px;
      border-radius: 4px;
      cursor: pointer;
      color: #a6adc8; /* Catppuccin Subtext0 */
      position: relative;
    }
    
    .channel-item:hover {
      background-color: #313244; /* Catppuccin Surface0 */
      color: #cdd6f4; /* Catppuccin Text */
    }
    
    .channel-item.active {
      background-color: #45475a; /* Catppuccin Surface1 */
      color: #cdd6f4; /* Catppuccin Text */
    }
    
    .channel-icon {
      color: #a6adc8; /* Catppuccin Subtext0 */
      font-size: 18px;
    }
    
    .channel-name {
      font-size: 14px;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
      flex: 1;
    }
    
    .unread-badge {
      background-color: #f5c2e7; /* Catppuccin Pink */
      color: #11111b; /* Catppuccin Crust */
      font-size: 12px;
      padding: 1px 6px;
      border-radius: 10px;
      min-width: 18px;
      text-align: center;
    }
    
    .user-panel {
      padding: 10px;
      background-color: #11111b; /* Catppuccin Crust */
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    
    .user-info {
      display: flex;
      align-items: center;
      gap: 8px;
    }
    
    .user-avatar-small {
      width: 32px;
      height: 32px;
      border-radius: 50%;
      overflow: hidden;
      position: relative;
    }
    
    .user-avatar-small img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }
    
    .status-indicator {
      position: absolute;
      width: 10px;
      height: 10px;
      border-radius: 50%;
      bottom: 0;
      right: 0;
      border: 2px solid #11111b; /* Catppuccin Crust */
    }
    
    .status-indicator.online {
      background-color: #a6e3a1; /* Catppuccin Green */
    }
    
    .status-indicator.idle {
      background-color: #f9e2af; /* Catppuccin Yellow */
    }
    
    .status-indicator.dnd {
      background-color: #f38ba8; /* Catppuccin Red */
    }
    
    .status-indicator.offline {
      background-color: #6c7086; /* Catppuccin Overlay0 */
    }
    
    .user-name-container {
      display: flex;
      flex-direction: column;
    }
    
    .username {
      font-size: 14px;
      font-weight: 600;
      color: #cdd6f4; /* Catppuccin Text */
    }
    
    .user-tag {
      font-size: 12px;
      color: #a6adc8; /* Catppuccin Subtext0 */
    }
    
    .control-button {
      background: none;
      border: none;
      color: #a6adc8; /* Catppuccin Subtext0 */
      cursor: pointer;
      font-size: 16px;
      width: 24px;
      height: 24px;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    
    /* Main content area */
    .main-content {
      background-color: #1e1e2e; /* Catppuccin Mocha base */
      display: flex;
      flex-direction: column;
    }
    
    .channel-header {
      padding: 12px 16px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-bottom: 1px solid #313244; /* Catppuccin Surface0 */
    }
    
    .channel-info {
      display: flex;
      align-items: center;
      gap: 8px;
    }
    
    .channel-info h2 {
      font-size: 16px;
      font-weight: 600;
    }
    
    .channel-actions {
      display: flex;
      align-items: center;
      gap: 16px;
    }
    
    .action-button {
      background: none;
      border: none;
      color: #a6adc8; /* Catppuccin Subtext0 */
      cursor: pointer;
      font-size: 14px;
      display: flex;
      align-items: center;
      gap: 4px;
    }
    
    .search-container {
      display: flex;
      align-items: center;
      background-color: #313244; /* Catppuccin Surface0 */
      border-radius: 4px;
      overflow: hidden;
    }
    
    .search-container input {
      background-color: transparent;
      border: none;
      padding: 6px 10px;
      color: #cdd6f4; /* Catppuccin Text */
      font-size: 14px;
      width: 180px;
    }
    
    .search-container input:focus {
      outline: none;
    }
    
    .search-button {
      background: none;
      border: none;
      color: #a6adc8; /* Catppuccin Subtext0 */
      cursor: pointer;
      padding: 6px 10px;
    }
    
    .message-area {
      flex: 1;
      overflow-y: auto;
      padding: 16px;
      display: flex;
      flex-direction: column;
      gap: 16px;
    }
    
    .message {
      display: flex;
      gap: 16px;
    }
    
    .message-avatar {
      width: 40px;
      height: 40px;
      border-radius: 50%;
      overflow: hidden;
      flex-shrink: 0;
    }
    
    .message-avatar img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }
    
    .message-content {
      flex: 1;
      display: flex;
      flex-direction: column;
      gap: 4px;
    }
    
    .message-header {
      display: flex;
      align-items: center;
      gap: 8px;
    }
    
    .message-author {
      font-weight: 600;
      font-size: 14px;
    }
    
    .message-time {
      color: #a6adc8; /* Catppuccin Subtext0 */
      font-size: 12px;
    }
    
    .message-text {
      font-size: 14px;
      line-height: 1.4;
      color: #cdd6f4; /* Catppuccin Text */
    }
    
    .message-attachments {
      margin-top: 8px;
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
    }
    
    .message-attachment {
      max-width: 400px;
      max-height: 300px;
      border-radius: 8px;
      cursor: pointer;
      object-fit: cover;
    }
    
    .message-input-container {
      padding: 16px;
      border-top: 1px solid #313244; /* Catppuccin Surface0 */
    }
    
    .message-input-wrapper {
      background-color: #313244; /* Catppuccin Surface0 */
      border-radius: 8px;
      padding: 12px;
      display: flex;
      align-items: center;
      gap: 12px;
    }
    
    .message-input {
      flex: 1;
      background: none;
      border: none;
      color: #cdd6f4; /* Catppuccin Text */
      font-size: 14px;
    }
    
    .message-input:focus {
      outline: none;
    }
    
    .send-button {
      background: none;
      border: none;
      color: #cba6f7; /* Catppuccin Mauve */
      cursor: pointer;
      font-size: 18px;
    }
    
    /* Users sidebar */
    .users-sidebar {
      background-color: #181825; /* Catppuccin Mantle */
      border-left: 1px solid #313244; /* Catppuccin Surface0 */
      overflow-y: auto;
    }
    
    .users-container {
      padding: 16px 8px;
    }
    
    .user-category {
      margin-bottom: 16px;
    }
    
    .user-category h3 {
      color: #a6adc8; /* Catppuccin Subtext0 */
      font-size: 12px;
      font-weight: 600;
      padding: 0 8px;
      margin-bottom: 8px;
    }
    
    .user-item {
      padding: 6px 8px;
      display: flex;
      align-items: center;
      gap: 10px;
      border-radius: 4px;
      cursor: pointer;
    }
    
    .user-item:hover {
      background-color: #313244; /* Catppuccin Surface0 */
    }
    
    .user-name {
      font-size: 14px;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }
  </style>