### NEXT JS

pnpx create-next-app@latest

###Commande Prisma

pnpm install prisma -D

pnpx prisma init

pnpx prisma migrate dev --name init

pnpm add @prisma/client

pnpx prisma generate

### AUTRES

pnpx prisma migrate dev --name added_model

pnpx  prisma migrate reset

pnpx prisma db pull

### Dependance 

pnpm install bcryptjs

pnpm install jsonwebtoken

pnpm install @prisma/client @supabase/ssr @supabase/supabase-js dotenv next react react-dom react-hook-form react-hot-toast zod && npm install -D @types/node @types/react @types/react-dom autoprefixer eslint eslint-config-next postcss prisma tailwindcss ts-node typescript

pnpm add @supabase/supabase-js next react react-dom typescript @types/react @types/react-dom tailwindcss uuid && pnpm add -D @types/node @types/uuid

lsof -i :3009

kill -9 41983

### Mes Server


// Gestion des erreurs de démarrage du serveur
const startServer = async () => {
  try {
    // Vérifie d'abord la connexion à Supabase
    const isConnected = await checkSupabaseConnection();
    if (!isConnected) {
      console.log('⚠️  Warning: Server starting without Supabase connection');
    }

    await new Promise((resolve, reject) => {
      const server = app.listen(port, () => {
        console.log(`✅ Server is running on port ${port}`);
        console.log(`📡 API Status:`);
        console.log(`   - Server: Running`);
        console.log(`   - Database: ${isConnected ? 'Connected' : 'Disconnected'}`);
        console.log(`   - Environment: ${process.env.NODE_ENV || 'development'}`);
        resolve();
      });

      server.on('error', (error) => {
        if (error.code === 'EADDRINUSE') {
          console.error(`❌ Port ${port} is already in use`);
          console.log('🔄 Trying with a different port...');
          server.close();
          const newPort = port + 1;
          server.listen(newPort);
        } else {
          console.error('❌ Server error:', error);
          reject(error);
        }
      });
    });
  } catch (error) {
    console.error('❌ Failed to start server:', error);
    process.exit(1);
  }
};
 