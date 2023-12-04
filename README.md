from abc import ABC, abstractmethod
from datetime import datetime

# Classe abstrata para mensagens
class Mensagem(ABC):
    def __init__(self, conteudo, arquivo, formato):
        self.conteudo = conteudo
        self.arquivo = arquivo
        self.formato = formato
        self.data_envio = datetime.now()

    @abstractmethod
    def enviar(self, destinatario):
        pass

# Subclasses para tipos de mensagem específicos
class MensagemTexto(Mensagem):
    def enviar(self, destinatario):
        print(f"Enviando mensagem de texto para {destinatario}: {self.conteudo}")

class MensagemVideo(Mensagem):
    def __init__(self, conteudo, arquivo, formato, duracao):
        super().__init__(conteudo, arquivo, formato)
        self.duracao = duracao

    def enviar(self, destinatario):
        print(f"Enviando vídeo para {destinatario}: {self.conteudo}, Duração: {self.duracao} segundos")

class MensagemFoto(Mensagem):
    def enviar(self, destinatario):
        print(f"Enviando foto para {destinatario}: {self.conteudo}")

class MensagemArquivo(Mensagem):
    def enviar(self, destinatario):
        print(f"Enviando arquivo para {destinatario}: {self.conteudo}")

# Classe para canais de comunicação
class CanalComunicacao(ABC):
    @abstractmethod
    def enviar_mensagem(self, mensagem, destinatario):
        pass

# Subclasses para canais específicos
class CanalWhatsApp(CanalComunicacao):
    def enviar_mensagem(self, mensagem, numero):
        print(f"Enviando mensagem via WhatsApp para {numero}")
        mensagem.enviar(numero)

class CanalTelegram(CanalComunicacao):
    def enviar_mensagem(self, mensagem, usuario):
        print(f"Enviando mensagem via Telegram para {usuario}")
        mensagem.enviar(usuario)

class CanalFacebook(CanalComunicacao):
    def enviar_mensagem(self, mensagem, usuario):
        print(f"Enviando mensagem via Facebook para {usuario}")
        mensagem.enviar(usuario)

class CanalInstagram(CanalComunicacao):
    def enviar_mensagem(self, mensagem, usuario):
        print(f"Enviando mensagem via Instagram para {usuario}")
        mensagem.enviar(usuario)

# Exemplo de uso
mensagem_texto = MensagemTexto("Bom dia?", None, None)
mensagem_video = MensagemVideo("Vídeo engraçado", "video.mp4", "mp4", 30)
mensagem_foto = MensagemFoto("Imagem bonita", "foto.jpg", "jpg")
mensagem_arquivo = MensagemArquivo("Documento importante", "documento.pdf", "pdf")

canal_whatsapp = CanalWhatsApp()
canal_telegram = CanalTelegram()
canal_facebook = CanalFacebook()
canal_instagram = CanalInstagram()

canal_whatsapp.enviar_mensagem(mensagem_texto, "+123456789")
canal_telegram.enviar_mensagem(mensagem_video, "@usuario_telegram")
canal_facebook.enviar_mensagem(mensagem_foto, "usuario_facebook")
canal_instagram.enviar_mensagem(mensagem_arquivo, "usuario_instagram")
