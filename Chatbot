import discord
from discord.ext import commands

# Configuración del bot
TOKEN = "TU_TOKEN_AQUI"  # Reemplaza con tu token de bot
intents = discord.Intents.default()
intents.message_content = True  # Necesario para leer el contenido de los mensajes
bot = commands.Bot(command_prefix="!", intents=intents)

# Evento: cuando el bot esté listo
@bot.event
async def on_ready():
    print(f"✅ Bot conectado como {bot.user}")

# Comando: !ping
@bot.command()
async def ping(ctx):
    await ctx.send("🏓 Pong! Latencia: {}ms".format(round(bot.latency * 1000)))

# Comando: !saludo (responde con un mensaje personalizado)
@bot.command()
async def saludo(ctx, nombre: str = "amigo"):  # Si no se proporciona un nombre, usa "amigo"
    await ctx.send(f"👋 ¡Hola, {nombre}! ¿Cómo estás?")

# Comando: !info (muestra información del usuario)
@bot.command()
async def info(ctx, miembro: discord.Member = None):
    miembro = miembro or ctx.author  # Si no menciona a nadie, usa el autor del mensaje
    embed = discord.Embed(title=f"Información de {miembro.name}", color=discord.Color.blue())
    embed.add_field(name="ID", value=miembro.id, inline=True)
    embed.add_field(name="Se unió el", value=miembro.joined_at.strftime("%d/%m/%Y"), inline=True)
    embed.set_thumbnail(url=miembro.avatar.url)
    await ctx.send(embed=embed)

# Evento: Responder automáticamente a "hola bot"
@bot.event
async def on_message(message):
    if message.author == bot.user:
        return  # Evita que el bot se responda a sí mismo
    
    if "hola bot" in message.content.lower():
        await message.channel.send("¡Hola! ¿Cómo estás? 😊")
    
    await bot.process_commands(message)  # Permitir que otros comandos funcionen

# Comando de grupo: !cool
@bot.group()
async def cool(ctx):
    """Dice si un usuario es cool.
    En realidad, solo verifica si se invoca un subcomando."""
    if ctx.invoked_subcommand is None:
        mensaje = f'No, {ctx.subcommand_passed} no es cool.' if ctx.subcommand_passed else 'Debes especificar a quién.'
        await ctx.send(mensaje)

# Subcomando: !cool bot
@cool.command(name='bot')
async def _bot(ctx):
    """¿Es el bot cool?"""
    await ctx.send('Yes, the bot is cool.')

# Comando: !joined (muestra cuándo un usuario se unió al servidor)
@bot.command()
async def joined(ctx, member: discord.Member):
    """Dice cuándo un miembro se unió."""
    await ctx.send(f'{member.name} se unió el {discord.utils.format_dt(member.joined_at)}')

# Iniciar el bot
bot.run("Token")
